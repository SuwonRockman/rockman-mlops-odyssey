# 🕸️ Season 2: Cognitive Search & GraphRAG (지식 그래프 검색)

이 과정은 파편화된 기업의 비정형 문서(매뉴얼, 리포트 등)에서 의미적 개체와 관계(Entity-Relationship)를 인공지능으로 구조화 추출하고, 이를 그래프 데이터베이스(Neo4j)에 적재하여 고도화된 하이브리드 검색망을 구축하는 **엔터프라이즈 GraphRAG 엔지니어링 실습 과정**입니다.

---

## 🗺️ 5단계 커리큘럼 로드맵 (Curriculum Roadmap)

각 단계별 폴더로 이동하여 이론 설명서(`01_theory.md`)와 실습 노트북(`02_[주제].ipynb`)을 학습하세요!

### 🧱 Phase 1: Data Preparation (비정형 데이터 정제)
*   **Step 01. [Structural Ingest & Parsing](./01_structural_ingest_parsing/)**
    *   정규표현식(Regex) 기반 구조적 마크다운 청킹 파이프라인 설계 및 Citations용 메타데이터 태깅 구현.

### 🕸️ Phase 2: Knowledge Extraction (지식망 추출)
*   **Step 02. [Industrial Knowledge Triplet Extraction](./02_knowledge_triplet_extraction/)**
    *   LLM Few-shot 프롬프팅 및 Pydantic JSON Schema 제어를 통한 Entity & Relation 트리플렛 추출기 구축.

### 🧠 Phase 3: DB Integration (Neo4j 적재)
*   **Step 03. [Neo4j Graph DB Integration](./03_neo4j_integration/)**
    *   Neo4j 속성 그래프 DB 모델링, Cypher 쿼리 언어 활용 대규모 그래프 적재 자동화 파이프라인 구현.

### 🔍 Phase 4: Hybrid Retrieval (하이브리드 검색 엔진)
*   **Step 04. [Cognitive Hybrid Retrieval](./04_cognitive_hybrid_retrieval/)**
    *   Dense Vector 유사도 스코어와 그래프 위상 매칭 가중치를 융합한 인지형 하이브리드 검색 엔진 설계.

### 🖥️ Phase 5: Search Interface (웹 포털 UI)
*   **Step 05. [Web Command Portal](./05_web_command_portal/)**
    *   Streamlit 및 NetworkX/PyVis 시각화 기법을 연동한 스마트팩토리 지식 검색 포털 UI 구축.
