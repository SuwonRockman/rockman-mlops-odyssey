# 🔌 FastAPI 비동기 ASGI 아키텍처 및 Docker 컨테이너화

[![Difficulty](https://img.shields.io/badge/Difficulty-Medium-orange.svg)](#) [![Topic](https://img.shields.io/badge/Topic-API%20Service-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 딥러닝 모델이나 에이전트를 실시간으로 구동하는 웹 서버를 설계할 때, 동기(Sync) 방식의 Flask/Django 대신 비동기(Async) 방식의 FastAPI를 쓰는 핵심적인 인프라 이점은 무엇일까요?

이 문서에서는 Uvicorn 기반의 **ASGI(Asynchronous Server Gateway Interface)** 이벤트 루프 동작 원리와 가볍고 안전한 배포를 위한 Docker 경량 멀티 스테이지 빌드 설계론을 다룹니다.

---

## 1. ASGI 비동기 이벤트 루프 동작

FastAPI는 파이썬의 `asyncio` 라이브러리를 극대화하여 싱글 스레드 환경에서도 수천 개의 I/O 바운드 요청(DB 쿼리, LLM API 호출 등)을 블로킹(Blocking) 없이 비동기 이벤트 루프로 동시 처리합니다.
