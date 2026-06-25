# 🤖 LangGraph 기반 상태 기계(State Machine)와 에이전트 라우팅

[![Difficulty](https://img.shields.io/badge/Difficulty-Medium%20High-orange.svg)](#) [![Topic](https://img.shields.io/badge/Topic-Multi--Agent-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 일반적인 단선적 체인(Sequential Chain) 구조의 에이전트는 무한 루프에 빠지거나, 에러 발생 시 자가 복구할 수 없습니다. 어떻게 복잡한 비즈니스 분기를 유기적인 그래프 구조로 정의하여 유연하게 대처할 수 있을까요?

이 문서에서는 유향 순환 그래프(Directed Cyclic Graph) 기반의 에이전트 오케스트레이션 프레임워크인 **LangGraph**의 동작 원리와 상태 관리(State Management) 이론을 다룹니다.

---

## 1. LangGraph의 핵심 아키텍처

LangGraph는 시스템의 흐름을 노드(Node), 엣지(Edge), 상태(State)의 3가지 요소로 표현합니다.

*   **State (상태)**: 그래프를 도는 데이터의 공유 가치(Shared Schema)를 정의합니다. 각 노드가 실행될 때마다 상태가 덮어씌워지거나 갱신(Reducer)됩니다.
*   **Node (노드)**: 특정 작업이나 에이전트의 판단 로직을 구현하는 함수입니다. 상태를 입력으로 받아 가공한 뒤 새로운 상태를 출력합니다.
*   **Edge (엣지)**: 노드와 노드의 연결을 규정합니다. 
    *   **Normal Edge**: 무조건 다음 노드로 이동하는 직선 연결.
    *   **Conditional Edge**: 현재 상태를 평가하여 동적으로 이동할 노드를 판정하는 조건부 라우팅 연결.
