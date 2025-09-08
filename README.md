# SAMUBOZO: 사무보조 플랫폼

![Build Status](https://img.shields.io/badge/build-passing-brightgreen) ![Coverage](https://img.shields.io/badge/coverage-85%25-yellow) ![License](https://img.shields.io/badge/license-MIT-blue)

MSA 기반으로 인사·근태·휴가·급여·전자결재·일정·쪽지·알림·챗봇을 통합 관리하는 업무·인사관리 플랫폼입니다.

---

## 📑 목차

1. [프로젝트 개요](#프로젝트-개요)  
2. [서비스 소개](#서비스-소개)  
3. [MSA 구성](#msa-구성)  
4. [공통 특징](#공통-특징)  
5. [배포 환경](#배포-환경)  
6. [기술 스택](#기술-스택)  
7. [아키텍처 & ERD](#아키텍처--erd)  
8. [설치 및 실행](#설치-및-실행)  
9. [API 문서](#api-문서)  
10. [팀 및 역할](#팀-및-역할)  
11. [프로젝트 일정 & WBS](#프로젝트-일정--wbs)  
12. [화면 설계](#화면-설계)  
13. [데모 & 프론트엔드](#데모--프론트엔드)  
14. [학습 내용 & 회고](#학습-내용--회고)  
15. [향후 계획](#향후-계획)  
16. [라이선스](#라이선스)  

---

## 프로젝트 개요

- **목적:** 분산·수작업 HR 업무를 MSA로 전환해 업무 속도·정확성 극대화  
- **기간:** 2025.06.20 – 2025.08.12  
- **팀 규모:** 5명  
- **내 역할 (신현국):** PM, 근태·휴가·전자결재 서비스 설계·구현·팀 일정 관리  

---

## 서비스 소개

수기 방식 한계와 과도한 SaaS 기능을 해결하기 위해, SAMUBOZO는 고객 니즈·해결 접근·기대 효과·차별성을 4분면 매트릭스로 설계했습니다.

| Needs (고객 니즈)                      | Approach (해결 접근)                             |
|---------------------------------------|-------------------------------------------------|
| • 과도한 기존 SaaS 비용 및 기능 문제  | • MVP 기반 핵심 기능 경량화                     |
| • 수기 업무 오류·누락·실수 위험       | • 출퇴근·급여 데이터 연계                       |
| • 전문성 부족·반복 업무 과중          | • 권한별 직관적 UI 제공                         |
| • 자동화 미비로 생산성 저하           | • 인사담당자 업무 자동화                        |

| Benefits (기대 효과)                   | Competition (차별성)                             |
|---------------------------------------|-------------------------------------------------|
| • 즉시 사용 가능한 기본 서비스 지원    | • 기존 SaaS 대비 낮은 도입 비용                  |
| • 업무 중심 설계 + MSA 기반 확장성 확보| • 경량 구조로 빠른 배포·테스트 가능               |
| • 자동화로 오류·누락 방지 → 생산성 향상| • 핵심 기능 집중 제공 → 복잡성 최소화            |

---

## MSA 구성

1. **핵심 인프라**  
   - config-service, discovery-service, gateway-service  
2. **인사·인증 도메인**  
   - auth-service, hr-service  
3. **근태·휴가 도메인**  
   - attendance-service, vacation-service  
4. **결재·증명 도메인**  
   - approval-service, certificate-service  
5. **업무 지원 도메인**  
   - schedule-service, message-service, notification-service, chatbot-service  
6. **급여 도메인**  
   - payroll-service  

---

## 공통 특징

- **문서화:** Swagger UI 통합 (tags-sorter, operations-sorter, display-request-duration)  
- **인증:** JWT 헤더 자동 주입  
- **버전 관리:** API 버전별 엔드포인트  

---

## 배포 환경

- Docker 컨테이너화 → Kubernetes (deploy/msa-chart)  
- Jenkins CI/CD → Argo CD GitOps  
- 중앙 설정: config-service, 디스커버리: discovery-service, 라우팅: gateway-service  

---

## 기술 스택

- 백엔드: Java 17, Spring Boot 3.3, QueryDSL, RabbitMQ, Redis, Feign, JWT  
- 프론트엔드: React 19, SCSS, Axios  
- 인프라: AWS (EKS, EC2, RDS, S3), Docker, Kubernetes, Argo CD, Jenkins  
- DB: MySQL (Amazon RDS), 빌드: Gradle  

---

## 아키텍처 & ERD

**시스템 아키텍처**  
<img src="https://github.com/user-attachments/assets/2f107192-e808-4b56-9770-affbb76327ed" width="800"/>

**ERD**  
<img src="https://github.com/user-attachments/assets/a31a1fa4-a9e7-4ef3-bd07-0789290142d6" width="800"/>

---

## 설치 및 실행

```bash
git clone https://github.com/samubozo/samubozo.git
cd samubozo
cp .env.example .env  # DB, JWT_SECRET 등 설정

# 백엔드
cd backend
./gradlew bootJar
java -jar build/libs/backend.jar

# 프론트엔드
cd ../front
npm install
npm start

# http://localhost:3000
```

---

## API 문서

### 도메인별 Swagger UI

- **인사 관리**  
  - http://{DOMAIN}/auth-service/swagger-ui.html  
  - http://{DOMAIN}/hr-service/swagger-ui.html  

- **근태 / 휴가**  
  - http://{DOMAIN}/attendance-service/swagger-ui.html  
  - http://{DOMAIN}/vacation-service/swagger-ui.html  

- **결재 / 증명**  
  - http://{DOMAIN}/approval-service/swagger-ui.html  
  - http://{DOMAIN}/certificate-service/swagger-ui.html  

- **업무 지원**  
  - http://{DOMAIN}/schedule-service/swagger-ui.html  
  - http://{DOMAIN}/message-service/swagger-ui.html  
  - http://{DOMAIN}/notification-service/swagger-ui.html  
  - http://{DOMAIN}/chatbot-service/swagger-ui.html  

- **급여 관리**  
  - http://{DOMAIN}/payroll-service/swagger-ui.html  

> **특징:** MSA 12개 서비스 API 통합·알파벳순 정렬·응답 시간 표시·실시간 테스트

---

## 팀 및 역할

| 이름       | 역할                                 | 주요 기여 서비스                                 |
|------------|-------------------------------------|------------------------------------------------|
| **신현국** | PM / 근태·휴가·결재 서비스 개발     | attendance-service, vacation-service, approval-service |
| **김예은** | 백엔드 (인사·인증·증명서)           | auth-service, hr-service, certificate-service   |
| **이호영** | 프론트엔드 (일정·쪽지·알림·챗봇)    | schedule-service, message-service, notification-service, chatbot-service |
| **주영찬** | 백엔드 (급여·설정) / 문서화         | payroll-service, config-service, README 리뷰  |
| **(기타)** | 인프라·CI/CD / discovery·gateway    | discovery-service, gateway-service, Jenkinsfile, k8s 차트 |

---

## 프로젝트 일정 & WBS

1. 기획 → 요구사항 정의 → ERD·API 설계  
2. 백엔드·프론트 구현 → 통합 테스트 → 배포  
3. 발표 및 회고  

- WBS 전체 계획: https://shinhyeonguk.github.io/samubozo-project-wbs/wbs.html  

---

## 화면 설계

- Google Slides: https://docs.google.com/presentation/d/12ljI3Y9HnpEqJc-bQNK0Zh_hEZbqaf3ECvE7X-3j0RM  

---

## 데모 & 프론트엔드

### 프론트가 궁금하신가요?  
https://github.com/samubozo/samubozo-front  

### 사무보조 구동 영상  
[![Video 1](https://img.youtube.com/vi/fminNemR4aU/0.jpg)](https://youtu.be/fminNemR4aU)  
[![Video 2](https://img.youtube.com/vi/FNfunqiHYh8/0.jpg)](https://youtu.be/FNfunqiHYh8)  
[![Video 3](https://img.youtube.com/vi/I1nTGJL1h5I/0.jpg)](https://youtu.be/I1nTGJL1h5I)  
[![Video 4](https://img.youtube.com/vi/G7RX3c_EYRM/0.jpg)](https://youtu.be/G7RX3c_EYRM)  

---

## 학습 내용 & 회고

- MSA 통신: Feign Client 활용  
- JWT 무상태 인증 & Refresh 전략 구현  
- Spring Scheduler로 급여·연차 자동 계산  
- GitOps · 코드 리뷰 문화 정착  

---

## 향후 계획

- OAuth2 / SSO 연동  
- Grafana·Prometheus 모니터링 도입  
- 모바일 앱(iOS/Android) 버전 개발  
- ELK 스택 로그 분석 강화  

---

## 라이선스

MIT License © 2025 Samubozo Team  

> 문의 및 피드백은 GitHub 이슈로 남겨주세요.  
> 즐거운 개발 되세요!
