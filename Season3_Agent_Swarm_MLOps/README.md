# ⚙️ Season 3: Agent Swarm & MLOps (에이전트 군집 및 배포 자동화)

이 과정은 앞서 시즌 1에서 생성한 **반도체 CMP 예지보전 모델**과 시즌 2의 **정비 매뉴얼 GraphRAG 지식망**을 통합하는 자율 멀티 에이전트 시스템을 구축하고, 모델 성능을 실시간 감시하여 자동으로 재학습 및 배포하는 **프로덕션 레벨의 MLOps/LLMOps 엔지니어링 실습 과정**입니다.

---

## 🗺️ 5단계 커리큘럼 로드맵 (Curriculum Roadmap)

각 단계별 폴더로 이동하여 이론 설명서(`01_theory.md`)와 실습 노트북(`02_[주제].ipynb`)을 학습하세요!

### 🤖 Phase 1: Agent Collaboration (에이전트 협업)
*   **Step 01. [Agent Collaboration Architecture](./01_agent_collaboration/)**
    *   LangGraph 기반 상태 기계 설계, 조건부 분기(Conditional Edge)를 통한 예외 처리 분기 에이전트 군집 구축.

### 🔌 Phase 2: Production Service (마이크로서비스화)
*   **Step 02. [Production API Service](./02_production_api_service/)**
    *   비동기 FastAPI 웹 애플리케이션 개발, Docker 멀티스테이지 빌드를 통한 에이전트 가상화 환경 배포.

### 📊 Phase 3: Experiment Tracking (실험 추적)
*   **Step 03. [MLflow Tracking & Register](./03_mlflow_tracking/)**
    *   MLflow API 연동 모델 학습 파라미터/메트릭 실시간 기록 및 중앙 모델 레지스트리(Model Registry) 관리.

### 📉 Phase 4: Model Monitoring (지속적 모니터링)
*   **Step 04. [Data Drift & Monitoring](./04_data_drift_monitoring/)**
    *   Evidently AI 연동 실시간 데이터/모델 드리프트(Drift) 분석 보고서 자동화 및 대시보드 구축.

### 🚀 Phase 5: Pipeline & CI/CD (지속적 배포/재학습)
*   **Step 05. [Automated CI/CD & Retraining Pipeline](./05_automated_pipeline/)**
    *   GitHub Actions 연동 자동화 단위 테스트(Pytest), 데이터 변크 발생 시 모델 자동 재학습 파이프라인(CT/CD) 설계.
