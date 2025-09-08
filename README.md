# SAMUBOZO: 사무보조 플랫폼

🔗 프론트엔드 레포: https://github.com/samubozo/samubozo-front

---

## 📺 구동 영상

[![Demo 1](https://img.youtube.com/vi/fminNemR4aU/0.jpg)](https://youtu.be/fminNemR4aU)  
[![Demo 2](https://img.youtube.com/vi/FNfunqiHYh8/0.jpg)](https://youtu.be/FNfunqiHYh8)  
[![Demo 3](https://img.youtube.com/vi/I1nTGJL1h5I/0.jpg)](https://youtu.be/I1nTGJL1h5I)  
[![Demo 4](https://img.youtube.com/vi/G7RX3c_EYRM/0.jpg)](https://youtu.be/G7RX3c_EYRM)

---

## ⚠️ 서비스 접근 제한 안내

현재 AWS 등 클라우드 비용 문제와 보안상 이유로 실 서버 배포 및 로컬 실행이 제한되어 있습니다.  
따라서 위 영상을 통해 서비스를 확인해주시기 바랍니다.

1. 서비스 배포 중단  
   - 클라우드 비용 문제로 온라인 배포 일시 중단  
   - 실환경 URL 제공 불가  

2. 로컬 실행 제한  
   - Config Server 설정 정보(private repo) 비공개  
   - 13개 MSA 서비스 간 의존성으로 개별 실행 어려움  

---

## 📑 목차

1. [프로젝트 개요](#프로젝트-개요)  
2. [서비스 소개](#서비스-소개)  
3. [MSA 구성](#msa-구성)  
4. [공통 특징](#공통-특징)  
5. [배포 환경](#배포-환경)  
6. [기술 스택](#기술-스택)  
7. [아키텍처 & ERD](#아키텍처--erd)  
8. [API 문서](#api-문서)  
9. [팀 및 역할](#팀-및-역할)  
10. [프로젝트 일정 & WBS](#프로젝트-일정--wbs)  
11. [화면 설계](#화면-설계)  
12. [학습 내용 & 회고](#학습-내용--회고)  
13. [향후 계획](#향후-계획)  
14. [라이선스](#라이선스)  

---

## 프로젝트 개요

- **목적:** 분산·수작업 HR 업무를 MSA로 전환하여 업무 속도 및 정확성 극대화  
- **기간:** 2025.06.20 – 2025.08.12  
- **팀 규모:** 4명  
- **내 역할 (신현국):**  
  - PM: 일정·리스크 관리  
  - 서비스 설계·구현: 근태·휴가·전자결재

---

## 서비스 소개

<img src="https://github.com/user-attachments/assets/d014d437-5f36-46e8-8cb3-bfea17e2bb2c" width="100%" alt="서비스 소개 매트릭스"/>


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
- **버전 관리:** API 버전별 엔드포인트 분리  

---

## 배포 환경

- Docker 컨테이너화 → Kubernetes (deploy/msa-chart)  
- Jenkins CI/CD → Argo CD GitOps  
- 중앙 설정: config-service  
- 서비스 디스커버리: discovery-service  
- API 라우팅: gateway-service  

---

## 기술 스택

- **백엔드:** Java 17, Spring Boot 3.3, QueryDSL, RabbitMQ, Redis, Feign, JWT  
- **프론트엔드:** React 19, SCSS, Axios  
- **인프라:** AWS (EKS, EC2, RDS, S3), Docker, Kubernetes, Argo CD, Jenkins  
- **DB:** MySQL (Amazon RDS)  
- **빌드:** Gradle  

---

## 아키텍처 & ERD

**시스템 아키텍처**  
<img src="https://github.com/user-attachments/assets/2f107192-e808-4b56-9770-affbb76327ed" width="70%" alt="시스템 아키텍처"/>

**ERD**  
<img src="https://github.com/user-attachments/assets/a31a1fa4-a9e7-4ef3-bd07-0789290142d6" width="70%" alt="ERD"/>

---

## API 문서

### 도메인별 Swagger UI

- **인사 관리**  
  - `http://{DOMAIN}/auth-service/swagger-ui.html`  
  - `http://{DOMAIN}/hr-service/swagger-ui.html`  

- **근태 / 휴가**  
  - `http://{DOMAIN}/attendance-service/swagger-ui.html`  
  - `http://{DOMAIN}/vacation-service/swagger-ui.html`  

- **결재 / 증명**  
  - `http://{DOMAIN}/approval-service/swagger-ui.html`  
  - `http://{DOMAIN}/certificate-service/swagger-ui.html`  

- **업무 지원**  
  - `http://{DOMAIN}/schedule-service/swagger-ui.html`  
  - `http://{DOMAIN}/message-service/swagger-ui.html`  
  - `http://{DOMAIN}/notification-service/swagger-ui.html`  
  - `http://{DOMAIN}/chatbot-service/swagger-ui.html`  

- **급여 관리**  
  - `http://{DOMAIN}/payroll-service/swagger-ui.html`  

> **특징:** MSA 12개 서비스 API 문서 통합 · 알파벳순 정렬 · 응답 시간 표시 · 실시간 테스트

---

## 팀 및 역할

| 이름       | 역할                              | 주요 기여 서비스                                          |
|------------|-----------------------------------|-----------------------------------------------------------|
| **신현국** | PM / 근태·휴가·전자결재 서비스 개발 | - `attendance-service`: 출퇴근·연차 자동 계산<br>- `vacation-service`: 휴가 워크플로우<br>- `approval-service`: 전자결재 흐름 설계 |
| **김예은** | 백엔드 (인사·인증·증명서)          | - `auth-service`: JWT 인증<br>- `hr-service`: 직원·조직 관리<br>- `certificate-service`: PDF 증명서 생성 |
| **이호영** | 프론트엔드 (일정·쪽지·알림·챗봇)   | - `schedule-service` UI<br>- `message-service` 실시간 채팅<br>- `notification-service` SSE 알림<br>- `chatbot-service` 챗봇 인터페이스 |
| **주영찬** | 백엔드 (급여·설정) / 문서화        | - `payroll-service`: 급여 계산 로직<br>- `config-service`: 중앙 설정 관리<br>- README·기여 문서 리뷰 |

---

## 프로젝트 일정 & WBS

1. 기획 → 요구사항 정의 → ERD·API 설계  
2. 백엔드·프론트 구현 → 통합 테스트 → 배포  
3. 발표 및 회고  

- WBS 전체 계획:  
  https://shinhyeonguk.github.io/samubozo-project-wbs/wbs.html  

---

## 화면 설계

- Google Slides:  
  https://docs.google.com/presentation/d/12ljI3Y9HnpEqJc-bQNK0Zh_hEZbqaf3ECvE7X-3j0RM  

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

> 문의 및 피드백은 GitHub Issue로 남겨주세요.  
> 즐거운 개발 되세요!
