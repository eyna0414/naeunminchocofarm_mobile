### 📌 프로젝트 개요

NaeunMinChocoFarm 백엔드는 스마트팜 통합 플랫폼의 핵심 로직과 API를 담당하는 서버 애플리케이션입니다. React 및 React Native 기반의 웹/모바일 앱과 통신하며, **농장(Farm), 구역(Section), 센서(Sensor), 환경값(습도, 온도, 일조량 등)**을 관리하는 기능을 제공합니다.

---

### 🛠 기술 스택

| 분류 | 내용 |
| --- | --- |
| 언어 | Java 17 |
| 프레임워크 | Spring Boot 3.x |
| ORM/DB 매핑 | MyBatis |
| DB | MariaDB |
| 보안 | Spring Security + JWT |
| 웹소켓 | STOMP 기반 WebSocket 구현 |
| 문서화 | Swagger (선택 적용 가능) |
| 기타 | DTO 계층 분리, 예외처리 모듈화, 파일 업로드 지원 등 |

---

### 🧩 전체 아키텍처 구성

```
사용자 (Web/Mobile)
     ↓
[NaeunMinChocoFarm API 서버]
├─ 인증 (JWT 기반 로그인/회원가입)
├─ 관리자 기능 (Farm/Section/Sensor 등록 및 관리)
├─ 사용자 기능 (MyPage, 서비스 신청)
├─ 센서 데이터 조회 (습도, 일조량, 토양, 온도 등)
├─ 실시간 제어 (WebSocket 기반 자동 급수/어닝)
     ↓
[DB (MariaDB)]
```

---

### ✅ 구현 기능 상세

### 1️⃣ 인증 및 보안

- 회원가입/로그인 및 토큰 발급 (JWT)
- Role 기반 접근 제어 (`USER`, `ADMIN`)
- 전역 예외 처리 및 인증 예외 커스터마이징

### 2️⃣ 스마트팜 관리 기능

- **Farm / Section / Sensor CRUD**
- UUID 자동 생성 및 외래키 연결
- Farm에 대한 Section, Section에 대한 Sensor 연결 구조 설계

### 3️⃣ 환경 센서 데이터 처리

- 습도(Humidity), 일조량(LDR), 온도(Temperature), 토양수분(SoilMoisture), CO₂ 등 조회 API
- 센서별 데이터 엔티티와 DTO 분리
- Chart 시각화를 위한 시간대별 조회 기능 구현

### 4️⃣ WebSocket 기반 실시간 처리

- WebSocket 연결 후 센서 데이터 수신
- 자동/수동 급수 시스템, 어닝 자동 제어 기능 포함
- `NcfFrame`, `NcfSubscribeHandler` 커스텀 메시지 구조 설계

### 5️⃣ 프로필 이미지 업로드

- `MultipartFile` 기반 이미지 업로드 처리
- 원본 이름과 서버 저장 파일명 관리
- 사용자 프로필과 연결되어 사용

### 6️⃣ 서비스 신청 및 관리

- 사용자 서비스 신청 기능
- 관리자 승인/반려 기능
- `ServiceApply`, `ServiceStatus` 도메인 분리 운영

---

### 📁 주요 디렉토리 구조 (패키지 기준)

```
com.naeunminchocofarm.ncf_api/
├─ smart_farm/               # Farm, Section, Sensor
├─ humidity/                 # 습도 센서 처리
├─ ldr/                      # 일조량 센서 처리
├─ soil_moisture/            # 토양수분 센서
├─ temperature/              # 온도 센서
├─ member/                   # 회원 인증, 이미지, 정보
├─ serviceApply/             # 서비스 신청
├─ lib/                      # JWT, 예외, 보안, 웹소켓 공통 모듈
└─ config/                   # 정적 리소스 설정 등
```
