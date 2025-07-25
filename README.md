
# 🎯 꿈담(Ggumdam) - 크라우드 펀딩 플랫폼

**창작자의 꿈을 담아내는 마이크로서비스 기반 크라우드 펀딩 플랫폼**

---

## 🧭 프로젝트 개요

`꿈담(Ggumdam)`은 창작자가 자유롭게 프로젝트를 등록하고, 사용자는 후원을 통해 이를 실현할 수 있도록 돕는 웹 기반 크라우드 펀딩 플랫폼입니다.

* **창작자는 아이디어를 등록하고 후원자를 모집**합니다.
* **사용자는 관심 있는 프로젝트에 펀딩 참여**를 합니다.
* **플랫폼은 펀딩, 결제, 보상, 쿠폰 등 전반적인 흐름을 지원**합니다.


---
⚙️ 사용 기술 스택
#### Backend
* Java 17, Spring Boot 3
* Spring Security (OAuth2.0 + 자체 회원가입)
* Spring Data JPA + MySQL
* Redis, Kafka (이벤트 기반 아키텍처)
* Elasticsearch (검색 기능)
* Docker + Spring Cloud Gateway (MSA)
* Logback + ELK Stack + Filebeat (로그 수집/분석)

#### Frontend
* React.js (CRA)
* Axios + Interceptor (JWT 관리)
* React-Router, React Hooks
* Styled CSS + Custom Component Design

---
## 🛠️ Microservices Architecture

| 계층                | 기술 스택                                                      |
| :------------------ | :------------------------------------------------------------- |
| Frontend            | `React`                                                        |
| Backend             | `Spring Boot (Java 17)`                                        |
| DB                  | `MySQL`                                                        |
| API Gateway         | `Spring Cloud Gateway`                                         |
| Service Discovery   | `Eureka`                                                       |
| Messaging           | `Apache Kafka` (회원가입 이벤트 처리)                          |
| Logging & Monitoring| `ELK Stack` (Elasticsearch, Logstash, Kibana)              |
| Deployment          | `Docker`, `Docker Compose`                                     |

### 🌐 서비스 구성 및 포트 매핑

| 포트   | 서비스 이름         | 설명                | 연결 DB 포트 |
| :----- | :------------------ | :------------------ | :----------- |
| `3000` | `React Frontend`    | 사용자 웹 인터페이스 | -            |
| `9000` | `Gateway Service`   | API Gateway         | -            |
| `10000`| `Eureka Service`    | 서비스 디스커버리   | -            |
| `8000` | `Auth Service`      | 인증(JWT, OAuth2), Kafka Producer | `3008` (auth-db) |
| `8005` | `User Service`      | 사용자 정보, 쿠폰 관리 | `3307` (user-db) |
| `8006` | `Project Service`   | 펀딩 프로젝트 등록/조회 | `3310` (project-db) |
| `8010` | `Order Service`     | 펀딩 주문, 예약 처리 | `3309` (order-db) |
| `8015` | `Payment Service`   | 결제 연동 (Iamport) | `3400` (payment-db) |

### 🔄 서비스 통신 구조 

```
graph TD
  A[React (3000)] --> B[API Gateway (9000)]
  B --> C[Eureka (10000)]
  B --> D[Auth Service (8000)]
  B --> E[User Service (8005)]
  B --> F[Project Service (8006)]
  B --> G[Order Service (8010)]
  B --> H[Payment Service (8015)]
  D --> |Kafka| E
```

🧩 Git Repository 구조
```
ggumdam-backend/
├── gateway-service/         # API Gateway
├── eureka-service/          # 서비스 디스커버리
├── auth-service/            # 로그인, OAuth2, JWT, Kafka 이벤트
├── user-service/            # 사용자 관리, Kafka Consumer, 쿠폰 발급
├── project-service/         # 프로젝트 등록/조회
├── order-service/           # 펀딩 주문/예약
├── payment-service/         # 결제 처리
├── frontend/                # React 웹 프론트엔드
├── kafka/                   # Kafka/Zookeeper 설정
├── elk/                     # ELK 스택 구성
├── docker-compose.yml       # 전체 서비스 도커 통합
└── README.md
```
## 🌟 주요 기능 및 기술

### 🔐 인증 및 권한 관리

Spring Security + JWT 기반 사용자 인증

OAuth2.0 소셜 로그인 (카카오, 구글, 네이버)

Redis로 Refresh Token 저장, HttpOnly 쿠키 사용

### 📦 펀딩 프로젝트

프로젝트 등록/조회/수정

카테고리/검색 조건 필터링

상세 페이지 찜하기/공유하기 기능 구현

### 💳 결제 및 주문

Iamport API 연동 (간편 결제 기능)

사용자 펀딩 참여 → 주문 내역 저장

### 📨 Kafka 이벤트 기반 비동기 처리

Auth → User 서비스 간 Kafka 메시지 전파

회원가입 이벤트 → 자동 쿠폰 발급 로직 구성

Redis Queue 및 Kafka Consumer/Producer 기반

### 📈 ELK 로그 모니터링

logback-spring.xml에서 JSON 포맷 로그 출력

Filebeat → Logstash → Elasticsearch 전송

Kibana를 통해 실시간 로그 시각화 대시보드 구현

### 🧪 API 문서화

Swagger (OpenAPI 3.0) 적용

각 서비스에서 /swagger-ui/index.html로 접근 가능

### 🔗 프로젝트 링크
#### 📁 GitHub

백엔드: [ggumdam-back](https://github.com/parker0509/ggumdam-backend)
프론트엔드: [ggumdam-front](https://github.com/parker0509/ggumdam-front/tree/main)


### 🎯 프로젝트 결과 및 회고
이번 프로젝트를 통해 **MSA 구조** 에서의 실시간 비동기 처리, Kafka 이벤트 흐름 설계, 그리고 **로그 수집 시스템(ELK) 구성**까지 경험할 수 있었습니다. 
특히 회원가입 후 쿠폰 자동 발급이라는 작은 요구사항을 어떻게 확장 가능한 구조로 만들 수 있을지를 고민하면서,
동기/비동기 처리의 차이와 서비스 분리의 중요성을 실감했습니다.
또한 프론트와 백엔드를 함께 설계하며 데이터 흐름, JWT 보안 처리, UX 요소까지 고려하는 과정에서 협업형 사고와 실무 감각을 익힐 수 있었고, 실제 사용자 관점의 시나리오 설계에도 많은 인사이트를 얻었습니다.


### 📧 Contact
Email: coldwatergk@gmail.com
GitHub: https://github.com/parker0509
