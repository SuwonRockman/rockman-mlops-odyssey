# 🚀 CT/CD (Continuous Training / Continuous Deployment) 파이프라인

[![Difficulty](https://img.shields.io/badge/Difficulty-Medium%20High-orange.svg)](#) [![Topic](https://img.shields.io/badge/Topic-CI%2FCD%20Pipeline-blue.svg)](#)

> [!NOTE]
> **핵심 질문**: 모니터링 엔진이 데이터 드리프트 경보를 발생시켰습니다. 엔지니어가 수동으로 파이썬 스크립트를 돌려 다시 학습시키는 대신, 전체 시스템이 어떻게 유기적으로 연결되어 자동으로 재학습하고 신규 모델로 안전하게 배포(Blue-Green 배포 등)를 완결할 수 있을까요?

이 문서에서는 데이터 스트림 유입부터 모델 모니터링 ➔ 드리프트 탐지 ➔ 자동 학습 트리거 ➔ GitHub Actions 기반 CI/CD 배포 자동화에 이르는 MLOps의 최종 폐루프(Closed Loop) 설계 이론을 다룹니다.
