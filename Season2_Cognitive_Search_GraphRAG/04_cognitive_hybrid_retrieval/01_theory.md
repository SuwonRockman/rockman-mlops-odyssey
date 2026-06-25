# 🔍 하이브리드 검색망 (Vector + Graph) 스코어 계산 공식

[![Difficulty](https://img.shields.io/badge/Difficulty-High-red.svg)](#) [![Topic](https://img.shields.io/badge/Topic-Hybrid%20Retrieval-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 질문의 의미적 유사도만 계산하는 Vector Search와, 논리적 연결 고리를 추적하는 Graph Search를 어떻게 수학적으로 하나로 묶어 가장 정답에 가까운 지식 정보를 검색해 낼 수 있을까요?

이 문서에서는 고성능 인지 검색을 위한 **Vector 코사인 유사도**와 **그래프 페이지랭크(PageRank)/위상 구조 유사도**의 수학적 융합 알고리즘을 다룹니다.

---

## 1. 하이브리드 검색 스코어링 공식 (Hybrid Scoring)

질문 쿼리 $q$에 대해 특정 문서 청크 또는 노드 $d$의 최적 하이브리드 스코어 $S_{hybrid}(d, q)$는 벡터 임베딩 유사도 $S_{vector}$와 그래프 위상 근접도 $S_{graph}$의 선형 가중 결합(Linear Combination)으로 설계됩니다.

$$S_{hybrid}(d, q) = lpha \cdot S_{vector}(d, q) + (1 - lpha) \cdot S_{graph}(d, q)$$

* $S_{vector}(d, q) = \cos(	heta) = rac{ec{u}_d \cdot ec{v}_q}{\|ec{u}_d\| \|ec{v}_q\|}$: 코사인 벡터 유사도
* $S_{graph}(d, q)$: 질문 내 엔티티 노드로부터 너비 우선 탐색(BFS) 또는 개인화된 페이지랭크(Personalized PageRank)를 통해 도출된 위상 근접 확률 스코어
* $lpha \sim [0, 1]$: 가중치를 분배하는 하이퍼파라미터
