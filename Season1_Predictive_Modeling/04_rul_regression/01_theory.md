# ⏱️ 잔여 수명 예측(RUL Regression)의 회귀 이론 및 평가지표

[![Difficulty](https://img.shields.io/badge/Difficulty-Medium-orange.svg)](#) [![Topic](https://img.shields.io/badge/Topic-Regression-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 설비의 잔여 수명(RUL, Remaining Useful Life)을 예측할 때 단순히 처음부터 끝까지 선형 감소하게 수명을 정의해 버리면 어떤 문제가 발생할까요? 장비 초기에는 노화가 진행되지 않는 물리적 상식을 수학적으로 어떻게 타겟 라벨(Target Label)에 투영할 수 있을까요?

이 문서에서는 장비의 잔여 유효 수명을 모델링하기 위한 **Piecewise Linear RUL 타겟 설계법**과 회귀(Regression) 분석의 성능 평가를 위한 평가지표 수학 공식을 다룹니다.

---

## 1. Piecewise Linear RUL 타겟 설계 기법

회전 기계(터빈, CNC 모터 등)는 가동 초기에 마모나 손상이 전혀 없이 매우 건전한 상태를 유지합니다. 만약 처음 가동 시점부터 고장 시점까지를 일직선으로 RUL이 감소하게 정의(Simple Linear RUL)한다면, 모델은 초기 가동 단계에서도 불필요하게 수명이 줄어들고 있다고 오학습을 하게 됩니다.

이 문제를 해결하기 위해 고정된 최대 잔여 수명 임계값(Max RUL)을 설정하고, 초기 가동 기간에는 이 값을 평탄하게 유지한 후 특정 열화 시점부터 선형 감소시키는 **Piecewise Linear RUL** 방식을 적용합니다.

```text
RUL Target
  ^
Max|--------------\
RUL|               \
   |                \  (Linear Decay)
   |                 \
  0+------------------\----> Time (Cycle)
   |<-  Initial Run ->|<-- Wear Stage ->|
```

### 수학적 정의
가동 주기(Cycle)를 $t$, 고장 시점을 $t_{fail}$, 초기의 일정한 건전 상태 RUL 임계값을 $R_{max}$라 할 때, 실제 라벨로 제공되는 수명 $R(t)$는 다음과 같이 정의됩니다.

$$R(t) = \min \left( R_{max}, \ t_{fail} - t \right)$$

* $R_{max}$: 보통 기계의 사양과 물리 센서 거동의 변화 시작점을 모니터링하여 $120$ 혹은 $130$ 사이클 등으로 조율합니다.

---

## 2. RUL 예측 성능 회귀 평가 지표 (Metrics)

예측 잔여 수명 $\hat{y}_i$와 참값 $y_i$ 사이의 성능 차이를 측정하기 위한 주요 회귀 지표입니다.

### MSE (Mean Squared Error)
예측 오차의 제곱 합의 평균입니다. 큰 오차에 페널티가 제곱으로 부과되므로 이상치(Outlier)에 민감하게 작용합니다.
$$\text{MSE} = \frac{1}{n} \sum_{i=1}^n (y_i - \hat{y}_i)^2$$

### RMSE (Root Mean Squared Error)
MSE에 루트를 씌워 실제 데이터의 단위와 일치시킨 가장 널리 쓰이는 기본 지표입니다.
$$\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^n (y_i - \hat{y}_i)^2}$$

---

## 3. NASA C-MAPSS 산업용 특화 패널티 스코어 (Score)

산업 현장(예: 제트 엔진, 철강 압연 롤)에서는 **수명을 실제보다 더 길게 예측(Over-estimation)**하는 것이 수명을 더 짧게 예측(Under-estimation)하는 것보다 훨씬 치명적입니다. 실제 수명이 다해가는데 아직 많이 남았다고 오판하면 정비 예방 시점을 놓쳐 폭발이나 대형 다운타임 사고로 이어지기 때문입니다.

이를 반영하여 NASA 연구팀은 조기 정비를 유도하도록 **늦은 예측에 가중 페널티를 부과하는 비대칭 지수 스코어(Asymmetric Score)** 평가지표를 정의했습니다.

$$S = \sum_{i=1}^n s_i$$
$$s_i = \begin{cases} 
e^{-\frac{d_i}{13}} - 1 & \text{for } d_i < 0 \quad (\text{Under-estimation, 조기 예측}) \\ 
e^{\frac{d_i}{10}} - 1 & \text{for } d_i \ge 0 \quad (\text{Over-estimation, 늦은 예측}) 
\end{cases}$$

* $d_i = \hat{y}_i - y_i$ (예측값 - 실제값 오차)

### 시각적 특징
* **$d_i = +10$ (늦은 예측)** 일 때: $s_i = e^{1} - 1 \approx 1.718$ 페널티 부과.
* **$d_i = -10$ (조기 예측)** 일 때: $s_i = e^{-\frac{10}{13}} - 1 \approx -0.537$ (절대값 $0.537$) 페널티 부과.
* 즉, 수명이 더 많이 남았다고 늦게 정비하라고 알려주는 오류($d_i > 0$)에 대해 약 **3배 이상의 강한 페널티**를 매겨 정비 정합성을 보장합니다.
