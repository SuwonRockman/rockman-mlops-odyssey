# 📊 MLflow 모델 실험 관리 및 모델 레지스트리 아키텍처

[![Difficulty](https://img.shields.io/badge/Difficulty-Medium-orange.svg)](#) [![Topic](https://img.shields.io/badge/Topic-Model%20Management-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 수많은 실험과 파라미터 튜닝을 통해 가장 좋은 성능의 고장 분류 모델을 찾았습니다. 이 모델 파일과 학습 당시의 환경설정, 평가 메트릭(RMSE, F1) 등을 어떻게 표준화하여 일원적으로 추적하고 관리할 수 있을까요?

이 문서에서는 모델의 지속적인 이력 추적과 생애주기를 관리해 주는 MLOps 핵심 인프라인 **MLflow**의 동작 구조를 다룹니다.

---

## 1. MLflow의 4대 핵심 컴포넌트

*   **MLflow Tracking**: 모델 실험의 파라미터(하이퍼파라미터), 코드 버전, 매트릭(성능 지표), 아티팩트(학습된 모델 가중치 파일)를 로깅 및 시각화합니다.
*   **MLflow Models**: 모델 가중치 파일을 다양한 플랫폼(Docker, Kubernetes 등)에서 로드할 수 있도록 공통 포맷으로 패키징합니다.
*   **MLflow Model Registry**: 중앙 저장소에서 모델의 버전과 운영 단계(Staging ➔ Production ➔ Archived)를 제어합니다.
