<img src="https://capsule-render.vercel.app/api?type=waving&color=3ED4BE&height=150&section=header" />
<h1 align="center">🇰🇷 I'm Junghyeon Yoon</h1>
<h3 align="center">Building Secure & Reliable Systems | Backend Dev & InfoSec | Kotlin & Go Learner</h3>



# Backend Developer, Samoyed

병목을 수치로 확인하고, 설계 근거를 문서로 남기는 백엔드 개발자입니다.
Java/Spring을 중심으로 개발하고, Kotlin 전환과 Go·Python 서비스 개발도 진행하고 있어요.

- Tech Blog: https://samoyed-02.github.io
- Email: dbswjdgus888@naver.com

## Selected Impact

- 리버스 프록시에서 AI 분석 서버 병목을 측정하고, 2대 분산 구성의 효과가 없음을 실험으로 확인 (PickStranger)
- Circuit Breaker로 AI 서버 중단 시에도 응답 유지, 100 VU 부하에서 요청의 62%를 Fail-Open 처리 (PickStranger)
- 파싱 예외율 30~40% → 0%, 표본 50건 전건 일치 (Enlist-Korea)
- 출결 도메인 재설계를 GitHub Issue로 문서화하고 프론트·기획과 합의 (동아리 CMS)

## Projects

**PickStranger | 이상 접속 탐지 보안 미들웨어** (Go, gRPC, Redis)
2인 프로젝트 (2026.03~08). 리버스 프록시 설계, gRPC 연동, 성능 검증과 병목 분석을 담당했어요.
- 문제: AI 분석 서버 CPU가 185%까지 올라 에러율 29.07%, P95 5.03초 발생
- 검증: 1대/2대 단계별 부하 테스트로 처리 한계가 약 15건/초로 같음을 확인. 병목은 호스트 CPU 용량이었음
- 대응: 연속 5회 실패 시 30초간 AI 호출을 건너뛰는 Circuit Breaker 적용
- 결과: 패스스루 경로 P95 65ms (200 VU 기준). AI 장애 중에도 서비스 응답 유지
- 상세 회고: [ ] (블로그 글 링크)

**동아리 CMS | 출결 관리 시스템** (Java, Spring Boot, MySQL, Redis)
16인 프로젝트, 백엔드 파트 참여 (2026.06~08). ERD 설계, 권한 제어, 출결 도메인 API 구현을 담당했어요.
- 문제: 출결이 일정 FK에 묶여 일정 없는 날 출결 불가, 하루 여러 일정 때 귀속 충돌
- 대응: 출결에서 일정 FK를 제거하고 attendanceDate 기준 UK(userId, attendanceDate)로 1일 1회 보장
- 문서화: GitHub Issue #86에 재설계 근거와 트레이드오프 기록, 팀과 합의
- 검증: 단위·슬라이스 테스트 35건, Redis TTL 기반 중복 출결 1차 검증

**Enlist-Korea | 공공데이터 기반 군 입영 지원 플랫폼** (Java 17, Spring Boot, MySQL, Jsoup)
4인 프로젝트, 팀 리더 겸 백엔드 단독 담당 (2025.03~11).
- 백엔드 코드: https://github.com/Enlist-Korea/Enlist-korea/tree/feature/back/main-service
- 문제: 고정 인덱스 파싱이 병합 셀(rowspan)에서 깨져 예외율 30~40%
- 대응: 가상 2차원 매트릭스 버퍼로 병합 셀 복원, 헤더 텍스트 기반 동적 매핑
- 검증: 복합 표 50건을 원본과 1:1 수기 대조, 매핑 정합성 100%
- 설계: 파싱 계층과 DB 엔티티 계층 분리, 군별 가산점 규칙을 인터페이스로 추상화

**Guard-Up | 계약서 가이드 백엔드** (Python, FastAPI, PostGIS, Chroma)
한이음 ICT 공모전. OCR, 비식별화, RAG, 공공 API 파이프라인 구성 담당 [ ]

**남산뚜 | 남한산성 GPS 스토리텔링** (FastAPI, PostgreSQL/PostGIS, Redis)
한국관광데이터 공모전, 4인 팀에서 백엔드 담당 [ ] (수치나 결과가 있다면 추가)

도파민 보물섬 | 캠퍼스 보물찾기 웹 서비스 (FastAPI, SQLite, React, Vite)
6일 MVP 스프린트, 풀스택 단독 개발 (2026.04)
- 백엔드 코드: https://github.com/Samoyed-02/dopamine-treasure-backend
- 백엔드: 장소 조회, 코드 검증, 보물 숨기기, 응원 메시지 등록 API, 중복 획득 방지 로직, 관리자 승인·통계 API 구현
- 프론트: 기존 800줄 이상의 프론트 코드를 Vite + React 구조로 재구성하고 화면 구현
- 운영: 기한 2일 초과로 4/22 배포, 실제 학생 대상 이벤트 진행 (보상 기프티콘 10개 지급)

## Tech Stack

Backend: Java, Spring Boot, Spring Data JPA, Kotlin (전환 중), Go, gRPC, Python (FastAPI)
Database & Cache: MySQL, PostgreSQL/PostGIS, Redis
API & Docs: OpenAPI 3.x, Swagger, RFC 9457 Problem Details
Infra & Observability: Docker, Nginx (로드 밸런싱), k6, Prometheus, Grafana
Testing: JUnit 5, Mockito, MockMvc, Postman




<img src="https://capsule-render.vercel.app/api?type=waving&color=3ED4BE&height=150&section=footer" />
