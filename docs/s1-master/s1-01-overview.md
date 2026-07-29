# S1-01: 프로젝트 개요 및 기술스택

**최종 갱신:** 2026-07-29

## 프로젝트 개요

kbeauty10(KB10)은 한국을 방문하는 외국인 여행자에게 K-뷰티 미용의료(피부과 중심) 정보를 제공하는 큐레이션 웹서비스입니다. 특정 시술을 서울에서 받을 수 있는 병원 정보를 대가 없이 나열·소개하는 정보 사이트이며, 검색 의도 기반 롱테일 콘텐츠로 생성형 검색(GEO) 인용을 목표로 합니다.

- URL: https://kbeauty10.com
- 저장소: https://github.com/cyjung23/kb10 (Private)
- 문서 저장소: https://github.com/cyjung23/kb10_pub (Public)
- 지원 언어: English(기본), 한국어

## 기술스택

- 프레임워크: Next.js 16 (App Router, React 19, Turbopack)
- i18n: next-intl (en/ko, [locale] 라우팅)
- DB: Supabase PostgreSQL
- 인증: Supabase Auth (Email Provider, Confirm email ON)
- 호스팅: Vercel (자동 배포, GitHub main push 트리거)
- 개발환경: GitHub Codespaces (Linux Ubuntu, bash)
- 분석: GA4 (TBD), Naver Analytics (TBD)
- SEO: Google Search Console, Naver Search Advisor
- 백업: GitHub Actions (매일 KST 09:00 pg_dump, 90일 보존)

## Vercel 환경변수

- NEXT_PUBLIC_SUPABASE_URL
- NEXT_PUBLIC_SUPABASE_ANON_KEY
- SUPABASE_SERVICE_ROLE_KEY

## 독립성 명시 (중요)

KB10은 특정 병원과 법적·자본적 관계가 없는 독립 정보 사이트입니다. SCP(참의원 연계)와 달리, KB10은 어떤 병원으로부터도 광고 의뢰나 실적 연동 대가를 받지 않습니다.

- 병원으로부터 광고 의뢰를 받아 제작하는 콘텐츠가 아님 (병원 요청 광고 아님)
- 예약·상담·결제 등 환자 송객·중개 기능 없음
- 순위·비교·과장 표현, 전후사진·후기 배제
- 병원 정보는 대가 없이 객관적으로 나열
- 근거 판례: 대법원 2010도1763(합법), 2018도20928(위법)
- 상세 원칙은 별도 원칙 문서 참조 (s1-master/s1-05-principles.md)

## 문서 구조

| 폴더 | 내용 |
|------|------|
| s1-master/ | 프로젝트 개요, 정체성, 기술 스택, 원칙 |
| s2-data/ | 데이터 현황, changelog |
| s3-completed/ | 완료 작업 이력 |
| s4-active/ | 진행/보류 작업, 우선순위 |
| s5-decisions/ | 의사결정 로그 (DEC-001~) |
| s6-roadmap/ | 로드맵, 마일스톤, 백로그 |

---

*최초 생성: 2026-07-29*
