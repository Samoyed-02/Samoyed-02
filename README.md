<img src="https://capsule-render.vercel.app/api?type=waving&color=6F42C1&height=150&section=header" />

# Backend Developer, Samoyed
측정 가능한 지표와 설계 근거를 바탕으로 문제를 해결하는 백엔드 개발자입니다.
서버 개발을 기반으로 AI 기능을 실제 서비스에 붙여 보며, 장기적으로는 플랫폼 엔지니어로 성장하고 싶습니다.

[![Resume](https://img.shields.io/badge/RESUME-Google%20Docs-4285F4?style=for-the-badge&logo=googledocs&logoColor=white)](https://docs.google.com/document/d/여기에_이력서_ID)
[![Tech Blog](https://img.shields.io/badge/TECH%20BLOG-Hugo-FF4088?style=for-the-badge&logo=hugo&logoColor=white)](https://samoyed-02.github.io)
[![Contact](https://img.shields.io/badge/CONTACT-문의%20폼-4285F4?style=for-the-badge&logo=googleforms&logoColor=white)](https://docs.google.com/forms/d/e/1FAIpQLSe1T1azEFz7amKQgpDanZI_sCQxfrlsb_DAM3lypgMBOYLhjA/viewform)

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

**Guard-Up | 계약서 가이드 백엔드** (Python, FastAPI, Redis, ChromaDB)
한이음 ICT 공모전. OCR·비식별화·RAG 파이프라인 및 공공 API 연동 담당 (2026.04~10).

– 구현: CLOVA OCR 텍스트 추출, KLUE-NER + 정규표현식 기반 개인정보 비식별화, Redis 세션 격리
– 문제: 계약서 이미지에서 추출한 개인정보가 외부 API(GPT-4o)로 전송될 경우 정보 유출 위험
– 대응: 로컬에서 PII 토큰 치환(PERSON_001) 후 마스킹 텍스트만 외부 전송, 분석 완료 후 매핑테이블 즉시 파기
– RAG: nlpai-lab/KURE-v1 임베딩 + ChromaDB로 주택임대차보호법·판례 34건 벡터화, 유사 조항 검색
– 검증: 서버 startup 시 법률 데이터 자동 임베딩, Redis 세션 연결 및 헬스체크 200 응답 확인

남산뚜 | 걷다, 남한산성 GPS 도보 관광 서비스 (Java, Spring Boot, MySQL, Redis)
2026 관광데이터 활용 공모전 · 4인 팀 백엔드 담당 (2026.04~09).
- 담당: Story Mode, Nearby 배치 ETL, Offline Sync, 카카오 인증, Railway 배포
- 문제: 주변 정보를 요청마다 TourAPI에서 가져와 호출 한도에 걸리고 응답이 느림
- 대응: 스케줄 배치로 DB에 적재하고, 조회 API는 DB만 읽도록 변경
- 결과: 카카오 인증 가짜 코드 우회 취약점을 재현해 수정하고, 운영 로그인 정상 동작 확인

도파민 보물섬 | 캠퍼스 보물찾기 웹 서비스 (FastAPI, SQLite, React, Vite)
6일 MVP 스프린트, 풀스택 단독 개발 (2026.04)
- 백엔드 코드: https://github.com/Samoyed-02/dopamine-treasure-backend
- 백엔드: 장소 조회, 코드 검증, 보물 숨기기, 응원 메시지 등록 API, 중복 획득 방지 로직, 관리자 승인·통계 API 구현
- 프론트: 기존 800줄 이상의 프론트 코드를 Vite + React 구조로 재구성하고 화면 구현
- 운영: 기한 2일 초과로 4/22 배포, 실제 학생 대상 이벤트 진행 (보상 기프티콘 10개 지급)

## Tech Stack

### Backend
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring%20Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white)
![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![gRPC](https://img.shields.io/badge/gRPC-244C5A?style=for-the-badge&logo=grpc&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)

### Database & Cache
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)

### Infra & DevOps
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)
![Railway](https://img.shields.io/badge/Railway-0B0D0E?style=for-the-badge&logo=railway&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)

### Observability & Testing
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)
![k6](https://img.shields.io/badge/k6-7D64FF?style=for-the-badge&logo=k6&logoColor=white)




<img src="https://capsule-render.vercel.app/api?type=waving&color=6F42C1&height=150&section=footer" />
