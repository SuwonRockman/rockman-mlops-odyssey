# ⚖️ 클래스 불균형 해결(SMOTE) 및 도메인 피처 엔지니어링

[![Difficulty](https://img.shields.io/badge/Difficulty-Medium-orange.svg)](#) [![Topic](https://img.shields.io/badge/Topic-Feature%20Engineering-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 실제 제조 현장에서 장비의 '고장(Failure)' 데이터는 정상 거동 데이터에 비해 극도로 적습니다(보통 1% 미만). 이 상태로 분류 모델을 학습하면 모델은 모든 데이터를 정상으로 예측해 버립니다. 소수 클래스 데이터를 기하학적으로 어떻게 확장하여 왜곡을 해결할 수 있을까요?

이 문서에서는 불균형 데이터 분류 문제를 극복하기 위한 대표적인 오버샘플링 기법인 **SMOTE(Synthetic Minority Over-sampling Technique)**의 기하학적 작동 원리와 시계열 데이터 가공을 위한 통계적 피처 생성론을 다룹니다.

---

## 1. SMOTE (Synthetic Minority Over-sampling Technique)

단순히 소수 데이터를 복제하는 Random Over-sampling은 과적합(Overfitting) 문제를 야기합니다. SMOTE는 소수 클래스(Minority Class)의 가상 데이터를 특성 공간(Feature Space)상의 직선 보간을 통해 합성하여 이 문제를 우아하게 해결합니다.

```mermaid
graph LR
    A["기준 소수 데이터 $x_i$"] --> B["K-최근접 이웃(KNN) 탐색<br>동일 소수 클래스 중 이웃 $x_{zi}$ 선정"]
    B --> C["선분 상에 임의 보간법 적용<br>$x_{new} = x_i + \lambda(x_{zi} - x_i)$"]
    C --> D["합성 데이터 $x_{new}$ 생성"]
```

### SMOTE의 합성 수식
소수 클래스의 한 관측치 $x_i$를 선택하고, 그 이웃($k$-NN) 중 임의의 관측치 $x_{zi}$를 선택한 후, 두 벡터 사이의 임의의 한 점을 가상 데이터로 합성합니다.
$$x_{new} = x_i + \lambda (x_{zi} - x_i)$$
* $x_i$: 소수 클래스의 특정 인스턴스 벡터
* $x_{zi}$: $x_i$와 동일한 클래스 내 $k$개 근접 이웃 중 임의로 선택된 벡터
* $\lambda \sim U(0, 1)$: 0과 1 사이의 균등 분포에서 무작위로 샘플링한 난수 스칼라

이러한 선형 조합을 통해 다차원 특성 공간에서 소수 클래스 영역이 뭉개지지 않고 볼록 껍질(Convex Hull)을 형성하며 점진적으로 확장됩니다.

---

## 2. 평가 지표의 왜곡과 대안 지표

클래스 불균형 환경에서는 정확도(Accuracy)를 신뢰할 수 없습니다. 따라서 오차 행렬(Confusion Matrix)에 기반한 다음과 같은 지표를 활용합니다.

$$\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}$$

### 대안 평가지표
1. **정밀도 (Precision)**: 모델이 고장으로 예측한 것 중 실제 고장의 비율 (과도한 오경보 방지)
   $$\text{Precision} = \frac{TP}{TP + FP}$$
2. **재현율 (Recall / Sensitivity)**: 실제 고장 데이터 중 모델이 정상적으로 찾아낸 비율 (고장 미탐 방지)
   $$\text{Recall} = \frac{TP}{TP + FN}$$
3. **F1-Score**: 정밀도와 재현율의 조화 평균 (두 지표가 균형을 이루는지 평가)
   $$\text{F1-Score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$$

---

## 3. 시계열 도메인 피처 엔지니어링

센서 스트림 데이터의 노이즈를 억제하고 추세를 반영하기 위해 다양한 윈도우 기반 통계 피처를 생성합니다.

*   **이동 평균 (Rolling Mean)**: 국소 잡음을 평활화하여 거시적 트렌드 파악.
*   **이동 표준편차 (Rolling Std)**: 설비의 진동이나 불안정성이 증가하는 징후 포착.
*   **지수 가중 이동 평균 (EMA)**: 최근 데이터에 더 높은 가중치를 부여하는 적응형 스무딩 기법.
    $$EMA_t = \alpha \cdot Y_t + (1 - \alpha) \cdot EMA_{t-1}$$
    * $\alpha = \frac{2}{N+1}$: 스무딩 인자
