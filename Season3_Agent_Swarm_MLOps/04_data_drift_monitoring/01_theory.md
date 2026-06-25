# 📉 데이터 드리프트(Data Drift)의 통계적 검증 및 Evidently AI

[![Difficulty](https://img.shields.io/badge/Difficulty-High-red.svg)](#) [![Topic](https://img.shields.io/badge/Topic-Model%20Monitoring-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 공장에 설치된 센서 하드웨어가 노후화되어 값이 미세하게 어긋나기 시작했습니다(Data Drift). 모델은 조용히 잘못된 고장 예측을 하고 있는데, 이 모델 성능의 '소리 없는 붕괴'를 수학적으로 어떻게 조기에 포착할 수 있을까요?

이 문서에서는 실시간 데이터의 분포 변동을 측정하기 위한 **Kolmogorov-Smirnov Test (KS-Test)** 검정 공식과 **PSI (Population Stability Index)** 지표의 통계적 수식을 다룹니다.

---

## 1. Kolmogorov-Smirnov Test (KS-Test)

KS-Test는 두 확률분포가 서로 같은 분포를 따르는지 검정하는 비모수 통계 방법입니다. 기준 학습 데이터(Reference)의 누적분포함수(CDF) $F_{ref}(x)$와 실제 들어오는 운영 데이터(Current)의 누적분포함수 $F_{curr}(x)$의 최대 수직 거리를 계산합니다.

$$D = \sup_x \left| F_{ref}(x) - F_{curr}(x) ight|$$

* $D$: 통계 검정량 (최대 수직 거리)
* 유의 수준 $p$-value가 임계치(보통 $0.05$ 또는 $0.01$) 미만으로 떨어지면 두 데이터의 분포가 유의미하게 달라진 것(Drift 발생)으로 진단합니다.

---

## 2. Population Stability Index (PSI)

PSI는 참조 집합(Expected)과 현재 집합(Actual) 사이의 변동 크기를 측정하는 계수입니다.
$$PSI = \sum_{b=1}^B \left( A_b - E_b ight) 	imes \ln\left( rac{A_b}{E_b} ight)$$
* $A_b$: 현재 버킷 $b$의 데이터 비율
* $E_b$: 참조 버킷 $b$의 데이터 비율
* **PSI 판정**:
  * $PSI < 0.1$: 안정적 (변동 거의 없음)
  * $0.1 \le PSI < 0.25$: 약간의 분포 변화 감지 (주의 필요)
  * $PSI \ge 0.25$: 심각한 분포 변동 (모델 재학습 필수)
