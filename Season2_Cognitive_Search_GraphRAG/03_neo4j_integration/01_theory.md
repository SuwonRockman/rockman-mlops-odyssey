# 🗄️ Neo4j 속성 그래프 DB 모델링 및 Cypher 쿼리 원리

[![Difficulty](https://img.shields.io/badge/Difficulty-Medium-orange.svg)](#) [![Topic](https://img.shields.io/badge/Topic-Graph%20Database-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 관계형 데이터베이스(RDB)에서 조인(Join) 연산이 늘어날수록 왜 쿼리 성능이 기하급수적으로 느려질까요? 관계를 물리적 포인터로 연결하여 속도를 기하급수적으로 상향시키는 그래프 DB(LPG 모델)의 이점과 Cypher 조작 언어의 작동 원리는 무엇일까요?

이 문서에서는 **Neo4j 그래프 데이터베이스**의 LPG(Labeled Property Graph) 데이터 모델과 멱등성을 보장하는 데이터 적재 쿼리 기술을 다룹니다.

---

## 1. LPG (Labeled Property Graph) 모델 구조

LPG 모델은 지식 데이터를 노드(Node), 관계(Relationship), 속성(Property), 라벨(Label)의 4개 요소로 표현합니다.

*   **Node (노드)**: 실체하는 개체(Entity). 하나 이상의 라벨(예: `:Equipment`, `:Component`)을 가질 수 있습니다.
*   **Relationship (관계)**: 노드와 노드를 연결하는 유향선(Directed Edge). 타입(예: `[:CONTAINS]`)이 정해져 있으며, 방향성이 존재합니다.
*   **Property (속성)**: 노드와 관계에 저장되는 Key-Value 형태의 메타데이터 (예: `{temperature: 80, timestamp: "2026-06-25"}`).

---

## 2. Cypher 멱등성 쿼리 (MERGE)

데이터 중복 적재를 막고 멱등성(Idempotency)을 유지하기 위해 `MERGE` 구문을 활용합니다.

```cypher
MERGE (e1:Equipment {name: $sub_name})
ON CREATE SET e1.created_at = timestamp()
MERGE (e2:Component {name: $obj_name})
MERGE (e1)-[r:HAS_COMPONENT]->(e2)
```
