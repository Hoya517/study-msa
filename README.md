# Spring Cloud 기반 MSA 학습 프로젝트

Spring Cloud를 활용하여 마이크로서비스 아키텍처(MSA)의 핵심 구성 요소를
학습하고, 간단한 주문/상품 서비스를 기반으로 서비스 간 통신, 인증, 설정
관리, 분산 추적, 이벤트 기반 아키텍처까지 단계적으로 실습한
프로젝트입니다.

---

# Project Goal

- Spring Cloud 기반 MSA 구조 이해
- 서비스 디스커버리 및 로드밸런싱
- API Gateway 기반 서비스 라우팅
- JWT 기반 인증 처리
- Config Server 기반 설정 중앙화
- Zipkin 기반 분산 추적
- Event Driven Architecture 이해

---

# Architecture

```
Client
  │
  ▼
API Gateway
  │
  ├── Auth Service
  ├── Order Service
  │       │
  │       ▼
  │   Product Service
  │
  └── Product Service


Infrastructure
──────────────
Eureka Server      : Service Discovery
Config Server      : Centralized Configuration
Zipkin             : Distributed Tracing
Event Stream       : Event Messaging
```

---

# Tech Stack

| Category  | Tech                 |
|-----------|----------------------|
| Language  | Java 21              |
| Framework | Spring Boot          |
| MSA       | Spring Cloud         |
| Discovery | Eureka               |
| Gateway   | Spring Cloud Gateway |
| Config    | Spring Cloud Config  |
| Security  | JWT                  |
| Tracing   | Micrometer + Zipkin  |
| Messaging | Spring Cloud Stream  |
| Build     | Gradle               |

---

# Service Components

## Eureka Server

서비스 디스커버리 서버

기능
- 서비스 등록
- 서비스 조회
- 로드밸런싱 기반 서비스 호출

주소: http://localhost:19090

---

## API Gateway

클라이언트 요청의 단일 진입점

기능
- 서비스 라우팅
- 글로벌 필터
- JWT 인증 처리

---

## Product Service

상품 조회 서비스

기능
- 상품 조회 API

---

## Order Service

주문 처리 서비스

기능
- 주문 조회
- Product Service 호출

---

## Config Server

마이크로서비스 설정 중앙 관리

주소: http://localhost:18080

---

## Zipkin

분산 추적 시스템

서비스 간 호출 흐름 추적

주소: http://localhost:9411

---

# 실행 방법

## 1. Zipkin 실행

```bash
docker run -d -p 9411:9411 openzipkin/zipkin
```

## 2. 서비스 실행 순서

1. Eureka Server
2. Config Server
3. Product Service
4. Order Service
5. API Gateway

---

# API Example

주문 조회

```
GET /order/1
```

호출 흐름

```
Client
→ Gateway
→ Order Service
→ Product Service
```

---

# Distributed Tracing

Zipkin을 통해 서비스 호출 흐름을 확인할 수 있습니다.

```
Client
→ Gateway
→ Order Service
→ Product Service
```

---

# Event Driven Architecture

Spring Cloud Stream을 이용하여 이벤트 기반 통신 구조를 학습했습니다.

예시 이벤트

```
Order Created Event
→ Inventory Service
→ Payment Service
→ Shipping Service
```

---

# Learning History

프로젝트는 다음 순서로 학습되었습니다.

1. Service Discovery (Eureka)
2. Client Side Load Balancing
3. API Gateway
4. JWT Authentication
5. Circuit Breaker
6. Config Server
7. Distributed Tracing (Zipkin)
8. Event Driven Architecture

---

# What I Learned

- MSA 환경에서 서비스 간 통신 구조
- Gateway 기반 인증 처리 방식
- Config Server를 통한 설정 중앙화
- Zipkin 기반 서비스 호출 추적
- 이벤트 기반 비동기 아키텍처

---

# Why MSA

MSA는 모든 상황에서 정답이 아니며, 서비스 규모와 조직 구조에 따라
선택되어야 합니다.

본 프로젝트는 MSA의 핵심 구성요소와 운영 구조를 학습하기 위해 단계적으로
구축되었습니다.

---

# Future Improvements

- Kafka 기반 이벤트 처리 확장
- Kubernetes 배포
- CI/CD 자동화
