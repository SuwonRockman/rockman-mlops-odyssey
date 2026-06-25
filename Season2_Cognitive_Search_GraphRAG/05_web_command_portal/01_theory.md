# 🖥️ Streamlit 기반 지식 검색 및 네트워크 시각화 구조

[![Difficulty](https://img.shields.io/badge/Difficulty-Medium-orange.svg)](#) [![Topic](https://img.shields.io/badge/Topic-Visualization-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 사용자에게 지식 그래프의 검색 결과와 노드들 간의 거대한 연관 관계 네트워크를 2D 인터랙티브 화면으로 어떻게 미려하고 동적으로 보여줄 수 있을까요?

이 문서에서는 파이썬 기반 웹 애플리케이션 프레임워크인 **Streamlit**과 자바스크립트 기반 동적 그래프 렌더러인 **PyVis / Vis.js**를 연동한 시각화 UI 컴포넌트 아키텍처를 다룹니다.

---

## 1. PyVis를 통한 그래프 레이아웃 렌더링

PyVis 라이브러리는 NetworkX 그래프 객체를 수신하여, 웹 브라우저의 Canvas 환경에서 물리 역학 법칙(Force-directed)이 가미된 Vis.js 물리 레이아웃 엔진으로 실시간 렌더링합니다.

*   **노드 척도화 (Node Scaling)**: Degree(연결선 수)가 높은 중요 노드를 물리적으로 더 크게 그립니다.
*   **엣지 방향성 (Edge Arrows)**: 관계의 인과관계를 화살표로 명시합니다.
