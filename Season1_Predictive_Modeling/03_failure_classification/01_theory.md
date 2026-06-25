# 🌲 XGBoost 트리 부스팅 알고리즘과 수학적 원리

[![Difficulty](https://img.shields.io/badge/Difficulty-High-red.svg)](#) [![Topic](https://img.shields.io/badge/Topic-Ensemble%20Learning-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 센서 스트림 데이터를 기반으로 설비 고장을 초 단위로 예측하는 분류기를 만든다면 왜 XGBoost가 최우선 선택지가 될까요? 기존의 단순 그래디언트 부스팅(GBM)과 수학적으로 어떻게 다르기에 뛰어난 일반화 성능과 속도를 보장할까요?

이 문서에서는 Taylor 2차 근사를 사용하는 극도로 최적화된 그래디언트 부스팅 알고리즘인 **XGBoost(Extreme Gradient Boosting)**의 목적 함수(Objective Function) 정형화 및 트리 가중치 계산의 수학적 유도 과정을 다룹니다.

---

## 1. XGBoost의 수학적 목적 함수 (Objective Function)

$k$번째 이터레이션에서 예측값 $\hat{y}_i^{(k)} = \hat{y}_i^{(k-1)} + f_k(x_i)$ 일 때, 학습 목적 함수 $\mathcal{L}^{(k)}$는 다음과 같이 손실 함수(Loss function)와 모델 복잡도에 대한 규제(Regularization)의 합으로 정의됩니다.

$$\mathcal{L}^{(k)} = \sum_{i=1}^n l(y_i, \hat{y}_i^{(k-1)} + f_k(x_i)) + \Omega(f_k)$$

* $f_k(x_i)$: $k$번째 단계에서 새로 학습할 약한 의사결정 트리 모델
* $\Omega(f_k) = \gamma T + \frac{1}{2} \lambda \sum_{j=1}^T w_j^2$: 트리의 노드 수 $T$와 각 단말 노드(Leaf Node)의 가중치 $w$에 가하는 L2 정규화 규제항

---

## 2. 테일러 2차 근사 (Taylor Expansion)를 이용한 목적 함수 변형

임의의 함수 $g(x + \Delta x)$는 Taylor 급수 전개에 의해 다음과 같이 근사할 수 있습니다.
$$g(x + \Delta x) \approx g(x) + g'(x)\Delta x + \frac{1}{2} g''(x) \Delta x^2$$

이를 목적 함수 $\mathcal{L}^{(k)}$에 대입하고, 이전 단계까지의 예측치 오차는 상수($const$)로 취급하여 제거하면 아래와 같은 2차 정형화된 목적 함수가 도출됩니다.

$$\mathcal{L}^{(k)} \approx \sum_{i=1}^n \left[ l(y_i, \hat{y}_i^{(k-1)}) + g_i f_k(x_i) + \frac{1}{2} h_i f_k^2(x_i) \right] + \Omega(f_k)$$
$$\tilde{\mathcal{L}}^{(k)} = \sum_{i=1}^n \left[ g_i f_k(x_i) + \frac{1}{2} h_i f_k^2(x_i) \right] + \gamma T + \frac{1}{2} \lambda \sum_{j=1}^T w_j^2$$

여기서 $g_i$(Gradient)와 $h_i$(Hessian)는 각각 손실 함수의 1차, 2차 도함수입니다.
* **Gradient**: $g_i = \frac{\partial l(y_i, \hat{y}_i^{(k-1)})}{\partial \hat{y}_i^{(k-1)}}$
* **Hessian**: $h_i = \frac{\partial^2 l(y_i, \hat{y}_i^{(k-1)})}{\partial (\hat{y}_i^{(k-1)})^2}$

---

## 3. 최적 가중치 $w_j^*$ 및 품질 평가 지표 $L_{split}$ 도출

데이터 인스턴스 $i$가 도달하는 단말 노드(Leaf)의 집합을 $I_j = \{i \mid q(x_i) = j\}$라 정의하고, 각 노드 내의 그래디언트 합을 $G_j = \sum_{i \in I_j} g_i$, 헤시안 합을 $H_j = \sum_{i \in I_j} h_i$ 라 치환합니다.
이를 통해 단말 노드 $j$ 기준으로 목적 함수를 묶을 수 있습니다.

$$\tilde{\mathcal{L}}^{(k)} = \sum_{j=1}^T \left[ \left( \sum_{i \in I_j} g_i \right) w_j + \frac{1}{2} \left( \sum_{i \in I_j} h_i + \lambda \right) w_j^2 \right] + \gamma T$$
$$\tilde{\mathcal{L}}^{(k)} = \sum_{j=1}^T \left[ G_j w_j + \frac{1}{2} (H_j + \lambda) w_j^2 \right] + \gamma T$$

### 최적 가중치 (Optimal Weight)
위 식은 $w_j$에 대한 2차 방정식이므로, 미분값이 0이 되는 지점을 구하면 단말 노드 $j$의 최적 예측값(가중치) $w_j^*$가 유도됩니다.
$$\frac{\partial \tilde{\mathcal{L}}^{(k)}}{\partial w_j} = G_j + (H_j + \lambda)w_j = 0$$
$$w_j^* = -\frac{G_j}{H_j + \lambda}$$

### 최적 목적 함수 스코어 (Optimal Value of Objective)
최적 가중치 $w_j^*$를 다시 목적 함수에 대입하면, 트리가 현재 분할을 통해 얻을 수 있는 최소 목적 함수값(스코어)을 얻습니다.
$$\tilde{\mathcal{L}}^{(k)*} = -\frac{1}{2} \sum_{j=1}^T \frac{G_j^2}{H_j + \lambda} + \gamma T$$

### 분할 품질 공식 (Split Criteria)
트리 탐색 시 어떤 피처를 기준으로 분할할지 결정하기 위해 분할 전후의 스코어 차이(Gain)를 계산합니다. 이 스코어가 가장 큰 피처와 임계값을 선택하여 나눕니다.

$$\text{Gain} = \frac{1}{2} \left[ \frac{G_L^2}{H_L + \lambda} + \frac{G_R^2}{H_R + \lambda} - \frac{(G_L + G_R)^2}{H_L + H_R + \lambda} \right] - \gamma$$

* $G_L, H_L$: 좌측 자식 노드의 그래디언트와 헤시안 합
* $G_R, H_R$: 우측 자식 노드의 그래디언트와 헤시안 합
* $\gamma$: 노드가 새로 생성될 때 추가되는 정규화 페널티(이득이 $\gamma$보다 크지 않으면 프루닝되어 분할되지 않음)
