# 🕸️ LLM 기반 지식 트리플렛(Triplet) 추출 이론

[![Difficulty](https://img.shields.io/badge/Difficulty-High-red.svg)](#) [![Topic](https://img.shields.io/badge/Topic-Information%20Extraction-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 비정형 텍스트 매뉴얼 내의 문장들 속에서 핵심 개체(Entity)와 그들 간의 의미적 관계(Relationship)를 어떻게 정밀하게 뽑아내어 컴퓨터가 해독 가능한 정량적 트리플렛(Triplet)으로 변환할 수 있을까요?

이 문서에서는 LLM(대형 언어 모델) 프롬프트 엔지니어링을 이용해 지식 그래프(Knowledge Graph)의 노드와 엣지를 생성하는 **삼항조(Entity-Relation-Entity) 추출**의 수학적 수식 스키마와 Few-shot 기법을 다룹니다.

---

## 1. 지식 트리플렛 (Knowledge Triplet)의 정의

트리플렛은 지식 네트워크의 최소 구성 단위로, 다음과 같이 삼항조(3-tuple)로 정의됩니다.
$$\mathcal{T} = (e_{subject}, \ r, \ e_{object})$$
* $e_{subject}$: 주체 엔티티 (Subject Entity - Node 1)
* $r$: 지식 관계 (Relationship - Edge)
* $e_{object}$: 객체 엔티티 (Object Entity - Node 2)

---

## 2. LLM 구조화 프롬프팅 및 JSON Mode 통제

일반적인 텍스트 출력 대신 시스템 스키마를 보장하기 위해 Pydantic 모델과 JSON Schema 제어를 결합하여 구조화된 출력을 유도합니다.

```json
{
  "entities": [{"name": "컴프레서", "type": "설비"}],
  "relationships": [{"source": "컴프레서", "target": "윤활유 펌프", "relation": "장착되어_있다"}]
}
```
