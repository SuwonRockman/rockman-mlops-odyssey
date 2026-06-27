# ==========================================
# Phase 2. FastAPI & Docker Service Dockerfile
# ==========================================
# 1. Builder Stage: 의존성 설치 및 휠 파일 빌드
FROM python:3.10-slim AS builder

WORKDIR /build

# 빌드에 필요한 도구 설치 (C 컴파일러 등 필요한 경우)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# requirements.txt 생성 및 설치
RUN echo "fastapi>=0.100.0\nuvicorn>=0.22.0\npydantic>=2.0\nhttpx>=0.24.0" > requirements.txt
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt


# 2. Runner Stage: 가볍고 안전한 실행 환경 구축
FROM python:3.10-slim AS runner

WORKDIR /app

# builder 스테이지에서 빌드된 패키지만 복사하여 용량 최소화
COPY --from=builder /install /usr/local

# 헬스체크에 필요한 최소한의 curl 설치
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    && rm -rf /var/lib/apt/lists/*

# 애플리케이션 코드 복사
COPY . /app

# 보안 가이드라인: 비루트(Non-root) 사용자 계정 생성 및 권한 부여
RUN useradd -u 1001 appuser && \
    chown -R appuser:appuser /app

# 권한이 없는 일반 사용자 계정으로 프로세스 가동
USER appuser

# 컨테이너 상태 모니터링을 위한 자체 헬스체크 선언
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:8000/health || exit 1

EXPOSE 8000

# FastAPI 구동 명령
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
