# 🚀 Phase 5: Automated CI/CD & Retraining Pipeline

데이터 분포 변동 감지 경보 수신 시, 자동으로 최신 데이터를 수집하여 반도체 CMP 예측 모델을 재학습시키고 GitHub Actions를 통해 FastAPI API 서버 컨테이너를 가동하여 무중단 무장애 배포하는 자동 배포 파이프라인을 실습합니다.

## 📂 파일 구성
*   `01_theory.md`: CT/CD 파이프라인의 이벤트 드리븐 트리거 구조 설계론
*   `02_automated_pipeline.ipynb`: 재학습 트리거 및 CI/CD 워크플로우 테스트 노트북
