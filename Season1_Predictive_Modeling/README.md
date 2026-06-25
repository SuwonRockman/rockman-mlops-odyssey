# 📈 Season 1: Predictive Modeling & Optimization (예측 모델링 & 최적화)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Language: Python](https://img.shields.io/badge/Language-Python-blue.svg)](#)
[![Framework: Scikit-learn & XGBoost](https://img.shields.io/badge/Framework-Scikit--learn%20%7C%20XGBoost-F7931E.svg)](#)

본 과정은 산업 도메인에서 수집되는 센서 시계열 데이터를 머신러닝으로 분석, 학습, 예측하고 설명 가능한 AI(XAI) 분석 기법까지 완주하는 데이터 과학 실습 모듈입니다.

---

## 🗺️ 5단계 커리큘럼 로드맵 (Curriculum Roadmap)

각 파일 링크를 클릭하여 해당하는 주피터 노트북 실습 파일로 바로 이동할 수 있습니다.

### 🧱 [Phase 1: Industrial Time-Series Preprocessing](./01_timeseries_preprocessing.ipynb)
센서 노이즈 필터링, 결측치 및 이상치 처리 기법을 배웁니다.
*   **실습 내용**: Rolling window 기법을 활용한 시간 스케일 변환, 칼만 필터(Kalman Filter) 및 이동평균을 통한 센서 노이즈 필터링 기법 구현.

### 🕸️ [Phase 2: Imbalanced Data & Feature Engineering](./02_imbalance_and_features.ipynb)
장애(Failure) 데이터가 매우 희소한 제조업 환경의 클래스 불균형 문제를 해결합니다.
*   **실습 내용**: SMOTE, ADASYN 등을 활용한 오버샘플링 기법 적용, 시간 도메인(Mean, Std, Skewness, Kurtosis) 및 주파수 도메인(FFT) 피처 추출.

### 🧠 [Phase 3: Equipment Failure Classification](./03_failure_classification.ipynb)
장애 유형(열적 장애, 과부하, 툴 마모 등)을 분류하는 멀티 클래스 예측 시스템을 구현합니다.
*   **실습 내용**: XGBoost, LightGBM, Random Forest 알고리즘 훈련 및 하이퍼파라미터 튜닝(GridSearch / Optuna).

### 🏢 [Phase 4: RUL (Remaining Useful Life) Regression](./04_rul_regression.ipynb)
설비가 고장나기 전까지 남은 가동 가능 시간(RUL)을 정교하게 예측합니다.
*   **실습 내용**: 시계열 회귀 모델링, RMSE 및 MAE 성능 평가 지표 최적화, 예측 추세선 가시화.

### ⚙️ [Phase 5: Explainable AI & Root Cause Analysis](./05_explainable_ai_rca.ipynb)
머신러닝 예측 결과에 대해 "왜 고장이 나는지" 설명하고 근본 원인을 추적합니다.
*   **실습 내용**: SHAP(Shapley Additive exPlanations) 값 추출, Summary plot, Dependence plot, Force plot 시각화 및 설비 고장 핵심 인자 식별.

---

## 🛠️ 실습 환경 준비
시즌 1 실습을 시작하기 위해 필요한 필수 패키지 목록입니다.

```bash
pip install -r requirements.txt
```
👉 필수 패키지는 **[requirements.txt](./requirements.txt)**를 확인하세요.
