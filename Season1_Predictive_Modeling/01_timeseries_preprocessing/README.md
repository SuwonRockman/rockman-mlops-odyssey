# 🧱 Phase 1: Industrial Time-Series Preprocessing

본 단계에서는 반도체 CMP 설비의 수치형 센서 시계열에 포함된 복잡한 잡음과 이상치, 그리고 네트워크 유실로 인한 결측치를 정제하는 실습을 진행합니다.

## 학습 주제
1. **이상치 및 결측치 탐지**: Z-score와 IQR을 이용한 튀는 값(Outlier) 제거 및 선형 보간법 적용.
2. **칼만 필터 (Kalman Filter)**: 가공 마찰에 따른 고주파 진동 성분을 확률 모델 기반으로 안정적으로 추정하는 1차원 칼만 필터 수학적 설계.
3. **Resampling**: 고주파(10Hz)의 원본 데이터를 분석 시스템 부하를 경감시키기 위해 1Hz(초 단위)로 다운샘플링하는 파이프라인 구축.

## 실습 파일
* [01_timeseries_preprocessing.ipynb](./01_timeseries_preprocessing.ipynb)
