🎯 꿈담(Ggumdam) - 크라우드 펀딩 플랫폼
창작자의 꿈을 담아내는 크라우드 펀딩 기반 웹 플랫폼

🧭 프로젝트 개요
꿈담(Ggumdam) 은 창작자들이 자신의 프로젝트를 등록하고, 후원자(사용자)로부터 펀딩을 통해 꿈을 실현할 수 있도록 돕는 크라우드 펀딩 플랫폼입니다. 사용자는 마음에 드는 프로젝트에 펀딩할 수 있으며, 창작자는 후원금으로 아이디어를 실현할 수 있습니다.

🛠️ Microservices Architecture Overview
계층	기술 스택
Frontend	React
Backend	Spring Boot (Java 17)
DB	MySQL
API Gateway	Spring Cloud Gateway
Registry	Eureka Discovery Service
Messaging	Apache Kafka (회원가입 이벤트 처리)
Logging	ELK Stack (Elasticsearch, Logstash, Kibana)
Deployment	Docker, Docker Compose

🌐 서비스 구성 및 포트 매핑
포트	서비스 이름	설명	연결 DB 포트
3000	React Frontend	사용자 웹 인터페이스	-
9000	Gateway Service	API Gateway	-
10000	Eureka Service	마이크로서비스 디스커버리	-
8000	Auth Service	로그인, JWT, OAuth2.0, Kafka 이벤트	3008 (auth-db)
8005	User Service	사용자 정보/프로필, 쿠폰 발급	3307 (user-db)
8006	Project Service	펀딩 프로젝트 등록/조회	3310 (project-db)
8010	Order Service	펀딩 주문 및 예약 처리	3309 (order-db)
8015	Payment Service	결제 처리 (Iamport 연동)	3400 (payment-db)

🔄 통신 구조 요약
mermaid
복사
편집
graph TD
  A[React (3000)] --> B[API Gateway (9000)]
  B --> C[Eureka (10000)]

  B --> D[Auth Service (8000)]
  B --> E[User Service (8005)]
  B --> F[Project Service (8006)]
  B --> G[Order Service (8010)]
  B --> H[Payment Service (8015)]

  D --> |Kafka| E
🧩 Git Repository 구조
bash
복사
편집
ggumdam-backend/
├── gateway-service/        # Spring Cloud Gateway
├── eureka-service/         # Eureka Server
├── auth-service/           # 로그인, OAuth2.0, Kafka Producer
├── user-service/           # 사용자 관리, Kafka Consumer, 쿠폰 발급
├── project-service/        # 펀딩 등록 및 조회
├── order-service/          # 주문 및 예약 처리
├── payment-service/        # 결제 처리
├── frontend/               # React 기반 웹 프론트엔드
├── kafka/                  # Kafka & Zookeeper 설정
├── elk/                    # ELK 스택 설정 (Elastic, Logstash, Kibana)
├── docker-compose.yml      # 전체 서비스 도커 컴포즈 실행 설정
└── README.md
🌟 핵심 기능
🔐 인증 및 권한
Spring Security + JWT 기반 인증

OAuth2.0 소셜 로그인 (카카오, 구글, 네이버)

📦 펀딩 프로젝트
프로젝트 등록/조회/수정

카테고리/조건별 필터링

💳 결제 및 주문
Iamport API 연동 간편 결제

펀딩 참여 및 주문 내역 조회

📨 Kafka 이벤트 처리
Auth 서비스 → User 서비스 간 회원가입 이벤트 전파

회원가입 완료 시 자동 쿠폰 발급 처리

📈 ELK 모니터링
Logstash → ElasticSearch → Kibana 대시보드 구축

실시간 로그 시각화로 시스템 분석 가능

🧪 API 문서화
Swagger(OpenAPI) 적용으로 각 서비스 API 명세 확인 가능

http://localhost:{port}/swagger-ui/index.html 경로에서 확인

✨ 담당 역할 (1인 개발)
시스템 설계 및 모든 마이크로서비스 개발

Kafka 기반 이벤트 시스템 구현

OAuth2.0 인증 흐름 구축 및 JWT 발급

Swagger/OpenAPI를 통한 API 문서화

Docker 기반 전체 서비스 통합 환경 구성

ELK 스택을 통한 로그 수집 및 시각화

🔗 프로젝트 링크
GitHub: https://github.com/parker0509/ggumdam-backend

Notion: 요청 시 제공 (기획 문서 및 일정 관리 포함)

📧 Contact
Email: coldwatergk@gmail.com

GitHub: https://github.com/parker0509
