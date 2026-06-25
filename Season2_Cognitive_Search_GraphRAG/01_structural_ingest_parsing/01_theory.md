# 📑 비정형 데이터 파싱 및 구조적 청킹 (Structural Chunking)

[![Difficulty](https://img.shields.io/badge/Difficulty-Medium-orange.svg)](#) [![Topic](https://img.shields.io/badge/Topic-Data%20Parsing-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 장비 매뉴얼 같은 복잡한 비정형 PDF, 텍스트 데이터가 들어왔을 때 단순히 글자 수 기준으로 무작위로 쪼개버리면(Character-based Split) 어떤 문제가 생길까요? 단락과 목차 구조를 파괴하지 않고 의미의 일관성을 유지하는 파싱 기법은 무엇일까요?

이 문서에서는 인공지능 지식망의 기초 공사가 되는 **구조적 청킹(Structural Chunking)** 설계론과 출처 추적(Citations)을 위한 메타데이터 태깅 이론을 다룹니다.

---

## 1. GIGO (Garbage In, Garbage Out) 방지론

RAG와 GraphRAG 시스템에서 생성 성능의 한계는 전적으로 데이터 인프라의 정밀성에 의존합니다. 문서 내의 제목, 하위 단락, 표(Table) 등이 깨진 상태로 임베딩 공간에 매핑되거나 지식 트리플렛으로 추출되면 LLM은 왜곡된 환각(Hallucination) 답변만을 생성하게 됩니다. 이를 차단하는 것이 파싱 단계의 목표입니다.

---

## 2. 정규표현식(Regex) 기반 구조적 마크다운 청킹

마크다운(Markdown)의 헤더 구조(`#`, `##`, `###`)를 파싱하여, 문서의 논리적 목차 트리 계층을 보존한 채로 쪼개는 기법입니다.

### 동작 알고리즘
1. 문서 전체의 마크다운 태그를 스캔합니다.
2. 헤더 태그를 기준으로 섹션의 시작과 끝 범위를 추출합니다.
3. 상위 헤더의 정보를 하위 텍스트 블록에 메타데이터로 상속합니다.
4. 너무 긴 본문 단락은 최대 토큰 제한(예: 500 Tokens) 하위에 두고, 중첩 슬라이딩 윈도우(Sliding Window)를 적용해 분절부의 정보 유실을 차단합니다.
