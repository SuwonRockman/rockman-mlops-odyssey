# ⚙️ Phase 5: Explainable AI & Root Cause Analysis

학습된 예측 분류 모델의 신뢰성을 보장하고 왜 모델이 고장을 감지했는지 설명하기 위해, **SHAP (Shapley Additive exPlanations)** 분석 기법을 실습합니다.

## 학습 주제
1. **SHAP 기여도 연산**: 트리 앙상블 기하학적 분석용 TreeExplainer 객체 선언 및 섑리 값(Shapley Values) 행렬 추출.
2. **글로벌 해석 (Global Explanation)**: 전체 센서 특성 중에서 가장 지배적인 영향력을 행사하는 핵심 센서 인자 파악 (Summary Plot).
3. **로컬 해석 및 근본 원인 역추적 (RCA)**: 개별 장비 고장 탐지 건에 대해 모델의 결정을 양/음의 인자 기여도로 분해하여 시각화 (Force Plot) 및 고장 원인 추적.

## 실습 파일
* [05_explainable_ai_rca.ipynb](./05_explainable_ai_rca.ipynb)
