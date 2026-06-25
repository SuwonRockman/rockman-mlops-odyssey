# 🕸️ Phase 2: Imbalanced Data & Feature Engineering

제조업 현업 데이터의 가장 큰 장애물인 극심한 고장 데이터의 클래스 불균형(Class Imbalance) 문제를 해소하고, 기계 상태를 묘사하는 피처들을 설계하는 단계입니다.

## 학습 주제
1. **시계열 피처 엔지니어링**: Rolling 통계값(표준편차 등) 및 물리 도메인 지식을 결합한 기계적 부하량(Mechanical Load) 변수 도출.
2. **주파수 대역 변환 (FFT)**: 고속 푸리에 변환(Fast Fourier Transform)을 활용하여 고주파 진동 신호의 주파수 대역별 에너지 밀도 분석.
3. **SMOTE 오버샘플링**: 소수의 고장 샘플을 지능적인 보간 기반 기법으로 오버샘플링하여 머신러닝 학습 결정 경계 안정화.

## 실습 파일
* [02_imbalance_and_features.ipynb](./02_imbalance_and_features.ipynb)
