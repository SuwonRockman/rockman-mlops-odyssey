# 📈 Industrial MLOps & Cognitive DS Masterclass

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Language: Python](https://img.shields.io/badge/Language-Python-blue.svg)](#)
[![Frameworks: MLflow & XGBoost](https://img.shields.io/badge/Framework-MLflow%20%7C%20XGBoost-FF6F00.svg)](#)

> **"Without data, you're just another person with an opinion."** - W. Edwards Deming
> (데이터가 없다면, 당신은 단지 의견을 가진 또 다른 사람일 뿐이다.)

이 마스터클래스(Track 2)는 실제 제조 현장 및 산업용 대규모 기계 설비 센서 스트림 데이터를 기반으로, 물리적 참값 추정(Preprocessing), 클래스 불균형 해소(Sampling), 장애 분류 및 잔여 수명 예측(Modeling)을 거쳐 최종적으로 예측 모델의 통계적 의사결정을 시각화(XAI)하고 지속 가능한 에이전트 시스템으로 자동화 및 운영하는 **산업용 MLOps 및 인지형 데이터 과학 실무 포트폴리오** 저장소입니다.

---

## 🎯 주요 아키텍처 및 하이라이트

1. **설비 센서 데이터 정밀 전처리 (Kalman Filtering)**: 통신 에러 및 물리 충격으로 튀는 계측 노이즈를 칼만 상태 방정식으로 평활화하여 참값 추정.
2. **소수 고장 데이터 극복 (Geometric SMOTE)**: 기하학적 선형 보간 합성 기법을 통해 1% 미만의 극소수 고장 클래스의 경계를 효과적으로 확장.
3. **고성능 머신러닝 모델링 (Taylor-optimized XGBoost)**: 목적 함수의 Taylor 2차 근사 분할 품질 공식을 분석하여 최적 가중치를 산정하는 기계 고장 이진 분류 구현.
4. **잔여 수명 추정 회귀 (Piecewise Linear RUL)**: 장비 가동 초기의 건전 상태를 반영하는 조각 선형 수명 라벨 설계 및 NASA 터보팬 엔진 평가용 비대칭 지수 패널티(Score) 분석.
5. **설명 가능한 AI를 통한 근본 원인 분석 (SHAP & LIME XAI)**: 협력 게임 이론의 섀플리 값 4대 공리를 활용하여 개별 센서 수치의 오작동 기여도를 시각화 및 분석.

---

## 🗺️ 커리큘럼 로드맵 (Curriculum Roadmap)

### 📈 [Season 1: Predictive Modeling & Optimization](./Season1_Predictive_Modeling/)
산업용 센서 데이터를 다루는 데이터 전처리부터 머신러닝 예측 모델 및 설명 가능한 AI(XAI) 분석까지 다루는 5단계 실습 과정입니다. 각 폴더로 이동하여 상세 이론서(`01_theory.md`)와 구현 코드(`02_[주제].ipynb`)를 확인하세요.

*   **Phase 1. Industrial Time-Series Preprocessing**: [Kalman Filter](./Season1_Predictive_Modeling/01_timeseries_preprocessing/)
    *   센서 신호 노이즈 제거, 칼만 가인 및 공분산 오차 추정, 선형/스플라인 데이터 보간 기법.
*   **Phase 2. Imbalanced Data & Feature Engineering**: [SMOTE Sampling](./Season1_Predictive_Modeling/02_imbalance_and_features/)
    *   불균형 분류 왜곡 극복, SMOTE 오버샘플링 기하 원리, 지수 이동 평균(EMA) 및 윈도우 통계 피처 추출.
*   **Phase 3. Equipment Failure Classification**: [XGBoost Classifier](./Season1_Predictive_Modeling/03_failure_classification/)
    *   장애 분류 의사결정 트리 학습, 테일러 2차 근사 목적 함수 손실 유도, 트리 분할 임계치 산정.
*   **Phase 4. RUL (Remaining Useful Life) Regression**: [RUL Predictive Modeling](./Season1_Predictive_Modeling/04_rul_regression/)
    *   장비 잔여 수명 조각 선형 타겟팅(Piecewise Linear), RMSE 회귀 학습, NASA 비대칭 페널티 스코어 분석.
*   **Phase 5. Explainable AI & Root Cause Analysis**: [SHAP & LIME XAI](./Season1_Predictive_Modeling/05_explainable_ai_rca/)
    *   블랙박스 의사결정 시각화, 섀플리 4대 공리(효율성, 대칭성, 더미, 가산성), LIME 국소 선형 설명 대리 모델.

---

### 🕸️ [Season 2: Cognitive Search & GraphRAG](./Season2_Cognitive_Search_GraphRAG/)
비정형 반도체 CMP 공정 설비 매뉴얼에서 Entity와 Relation 지식 트리플렛을 추출하고 Neo4j 그래프 데이터베이스에 적재하여 하이브리드 검색망을 구축하는 5단계 실습 과정입니다. (진행 중)

*   **Phase 1. Structural Ingest & Parsing**: [Markdown Chunking](./Season2_Cognitive_Search_GraphRAG/01_structural_ingest_parsing/)
    *   정규식 기반 마크다운 청킹, 출처용 메타데이터 태깅, 반도체 CMP 공정 매뉴얼 원본 데이터 적재.
*   **Phase 2. Knowledge Triplet Extraction**: [LLM Triplet Extraction](./Season2_Cognitive_Search_GraphRAG/02_knowledge_triplet_extraction/)
    *   LLM Few-shot 프롬프트 가이드라인 설계 및 JSON Schema 통제 기반 지식 삼항조 추출.
*   **Phase 3. Neo4j Graph DB Integration**: [Graph DB Modeling](./Season2_Cognitive_Search_GraphRAG/03_neo4j_integration/)
    *   LPG 속성 그래프 모델 구축 및 Cypher 멱등성 쿼리(MERGE) 대규모 지식 적재 자동화.
*   **Phase 4. Cognitive Hybrid Retrieval**: [Hybrid Retrieval](./Season2_Cognitive_Search_GraphRAG/04_cognitive_hybrid_retrieval/)
    *   Dense Vector 의미 유사도 및 그래프 네트워크 구조 위상 결합 하이브리드 검색 랭킹 계산.
*   **Phase 5. Web Command Portal**: [Streamlit Visual Portal](./Season2_Cognitive_Search_GraphRAG/05_web_command_portal/)
    *   Streamlit 및 Vis.js 물리 엔진 연동 인터랙티브 지식 그래프 시각화 정비 검색 포털 UI 빌드.


---

### ⚙️ [Season 3: Agent Swarm & MLOps](./Season3_Agent_Swarm_MLOps/)
CMP 예지보전 모델과 GraphRAG 조치 검색망을 결합하는 LangGraph 멀티 에이전트 협업 체계를 설계하고, 실시간 데이터 드리프트를 모니터링하여 자동 재학습 및 배포하는 5단계 MLOps 프로덕션 구축 과정입니다. (진행 중)

*   **Phase 1. Agent Collaboration**: [LangGraph Agent Swarm](./Season3_Agent_Swarm_MLOps/01_agent_collaboration/)
    *   유향 순환 그래프 기반 LangGraph 상태 기계 설계 및 조건부 라우팅 예외 처리 구현.
*   **Phase 2. Production API Service**: [FastAPI & Docker Service](./Season3_Agent_Swarm_MLOps/02_production_api_service/)
    *   비동기 ASGI 이벤트 루프 FastAPI 개발 및 Docker 멀티스테이지 컨테이너 가상화 배포.
*   **Phase 3. MLflow Tracking & Register**: [MLflow Experiment Tracker](./Season3_Agent_Swarm_MLOps/03_mlflow_tracking/)
    *   모델 파라미터/성능 지표 자동 로깅 및 중앙 모델 레지스트리 라이프사이클 관리.
*   **Phase 4. Data Drift & Monitoring**: [Evidently AI Monitor](./Season3_Agent_Swarm_MLOps/04_data_drift_monitoring/)
    *   Kolmogorov-Smirnov 검정 및 PSI 통계량 계산 기반 실시간 센서 분포 변동(Drift) 분석.
*   **Phase 5. Automated CI/CD & Retraining**: [CT/CD Pipeline](./Season3_Agent_Swarm_MLOps/05_automated_pipeline/)
    *   데이터 분포 변동 감지 시 자동 재학습(CT) 트리거 및 GitHub Actions 연동 자동화 배포(CD).

---



## 🛠️ 기술 스택 (Tech Stack)

### Core Machine Learning & Math
* **Frameworks:** XGBoost, PyTorch, Scikit-learn, Scipy, Pandas, Numpy
* **XAI Engine:** SHAP, LIME

### Infrastructure & Operations (To be updated in Season 3)
* **MLOps System:** MLflow, Evidently AI, FastAPI, Docker
* **Frontend:** Streamlit, Matplotlib, Seaborn

---
<div align="center">
  <i>Created with ❤️ by Jung Seyoon (SuwonRockman)</i>
</div>
