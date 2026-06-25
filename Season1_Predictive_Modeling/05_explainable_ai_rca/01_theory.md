# 🔍 설명 가능한 AI (XAI) 및 섀플리 값(Shapley Value)의 수학

[![Difficulty](https://img.shields.io/badge/Difficulty-High-red.svg)](#) [![Topic](https://img.shields.io/badge/Topic-Explainable%20AI-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 머신러닝 예측 모델이 공장의 특정 컴프레서 장비에 고장 장애 경보를 울렸습니다. 하지만 이 모델은 복잡한 블랙박스(Black-box)라 내부 의사결정을 알 수 없습니다. 현장 엔지니어가 납득하고 부품을 교체할 수 있도록 **"어떤 센서 수치가 고장 판단에 기여했는지"**를 기여도 금액처럼 투명하게 정량화할 수 있을까요?

이 문서에서는 협력 게임 이론(Cooperative Game Theory)에 기반하여 블랙박스 머신러닝 모델의 개별 예측치 기여도를 계산하는 최상위 XAI 기법인 **SHAP (SHapley Additive exPlanations)**의 수학적 이론과 근본 원인 분석(Root Cause Analysis) 방법론을 다룹니다.

---

## 1. 섀플리 값 (Shapley Value)

게임 이론에서 공동으로 하나의 목표(예측치)를 달성한 여러 플레이어(피처 센서들)에게 공평하게 성과를 배분하는 기여도 측정값입니다.

### 수학적 정의
전체 피처 집합 $F$에서 특정 피처 $i$의 기여도를 나타내는 섀플리 값 $\phi_i$는 피처 $i$를 제외한 모든 가능한 피처 조합 $S$에 대해, $i$가 추가되었을 때 발생하는 **한계 기여도(Marginal Contribution)**의 가중 평균으로 계산됩니다.

$$\phi_i = \sum_{S \subseteq F \setminus \{i\}} \frac{|S|! (|F| - |S| - 1)!}{|F|!} \left[ f(S \cup \{i\}) - f(S) \right]$$

* $F$: 전체 입력 특성(Features)의 집합
* $S$: 피처 $i$가 포함되지 않은 부분집합 (Coalition)
* $f(S)$: 피처 집합 $S$의 값들만 사용했을 때의 모델 예측 함수값
* $\frac{|S|! (|F| - |S| - 1)!}{|F|!}$: 부분집합 $S$의 크기에 따른 경우의 수 확률 가중치
* $f(S \cup \{i\}) - f(S)$: 피처 $i$가 추가됨으로써 기여한 순수 예측 변화량

---

## 2. 섀플리 값이 보장하는 4대 공리 (Axioms)

섀플리 값은 다음의 네 가지 수학적 조건을 동시에 유일하게 만족하는 기여도 계산법입니다.

1. **효율성 (Efficiency)**:
   각 특성 기여도의 총합은 전체 모델 예측치 $f(x)$와 평균 예측치 $E[f(x)]$의 차이와 같습니다.
   $$\sum_{i=1}^{|F|} \phi_i(x) = f(x) - E[f(x)]$$
2. **대칭성 (Symmetry)**:
   두 특성 $j$와 $k$가 모든 동맹 그룹에 대해 기여한 효과가 동일하다면, 그 기여 가치도 같습니다.
   $$\text{If } f(S \cup \{j\}) = f(S \cup \{k\}), \ \text{then } \phi_j = \phi_k$$
3. **더미 (Dummy / Null Player)**:
   어떤 특성이 모델의 예측에 전혀 아무런 영향도 미치지 못한다면, 그 기여도는 0입니다.
   $$\text{If } f(S \cup \{i\}) = f(S), \ \text{then } \phi_i = 0$$
4. **가산성 (Additivity)**:
   두 모델의 예측값을 더한 것의 기여도는 각 모델에서의 기여도 합과 같습니다.
   $$\phi_i(f + g) = \phi_i(f) + \phi_i(g)$$

---

## 3. SHAP와 LIME의 국소 모델 근사 비교

개별 관측치(Local)의 예측 배경을 설명하는 기법들의 장단점 비교입니다.

| 기법 | 수학적 설명 방식 | 장점 | 단점 |
| :--- | :--- | :--- | :--- |
| **SHAP** | 섀플리 값 이론의 4대 공리를 만족하는 가산적 특징 기여도(Additive Feature Attribution) 추정 | 유일하고 수학적으로 일관적인 정량 수치 보장. 트리 계열 전용 가속 알고리즘(TreeSHAP) 제공. | 연산량이 매우 많음 ($2^{|F|}$ 제곱승에 비례) |
| **LIME** | 예측 데이터 근처의 표본들을 샘플링하여 설명 가능한 단순 대리 모델(Surrogate Model) 국소 학습 | 설명 모델(예: 선형 회귀)을 통해 직관적인 기여 계수 해석 가능. | 데이터 샘플링 시 무작위성으로 결과가 매번 약간씩 바뀔 수 있음. |

### LIME의 최적화 정형화 식
$$g^* = \arg\min_{g \in G} \mathcal{L}(f, g, \pi_x) + \Omega(g)$$
* $\mathcal{L}(f, g, \pi_x)$: 오리지널 모델 $f$와 설명 모델 $g$의 로컬 유사도 $\pi_x$에 비례한 가중 손실 함수
* $\Omega(g)$: 설명 모델 $g$의 복잡도 규제항
