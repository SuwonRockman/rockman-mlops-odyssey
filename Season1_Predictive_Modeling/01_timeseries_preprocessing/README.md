# 🧱 Phase 1: Industrial Time-Series Preprocessing

본 단계에서는 반도체 CMP 설비의 수치형 센서 시계열에 포함된 복잡한 잡음과 이상치, 그리고 네트워크 유실로 인한 결측치를 정제하는 실습을 진행합니다.

---

## 📂 목차 (Contents)

- **`01_theory.md`**: 칼만 필터(Kalman Filter)의 상태 방정식, 관측 방정식의 수학적 증명 및 센서 노이즈 제거 원리
- **`02_timeseries_preprocessing.ipynb`**: 시계열 센서 이상치 탐지(IQR/Z-score), 데이터 보간(Interpolation) 및 MFC 유량 리샘플링 구현 실습 노트북

---

## 🛠️ 기술 스택 (Tech Stack)
- Python, Pandas, Numpy, Scikit-learn
- Jupyter Notebook
