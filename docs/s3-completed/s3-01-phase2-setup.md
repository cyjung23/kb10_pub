# Phase 2 완료 기록 — Next.js + next-intl 초기 세팅

*완료일: 2026-07-08*

## 완료 내용
- Next.js 16.2.10 + TypeScript + Tailwind v4 프로젝트 생성 (create-next-app, src-dir, app router, import alias @/*)
- next-intl 4.13.1 설치 및 다국어 설정
  - `src/i18n/routing.ts`: locales ["en","ko"], defaultLocale "en", localeDetection false
  - `src/i18n/request.ts`: 메시지 로딩 (../../messages/{locale}.json)
  - `next.config.ts`: createNextIntlPlugin 적용
  - `src/middleware.ts`: next-intl 기본 미들웨어 (SCP의 크롤링방어/slug정규화 로직은 제외, 향후 필요시 추가)
  - `messages/en.json`, `messages/ko.json`: 초기 샘플 키
- `src/app/[locale]/` 구조로 재배치 (layout.tsx, page.tsx). 루트 layout은 children 통과형
- 로컬 검증: /en, /ko 정상 작동. 루트(/)는 en 고정 리다이렉트 확인 (curl Accept-Language 테스트 통과)
- git 커밋·푸시 완료 (kb10 저장소, 커밋 b8c536d)

## 버전 참고 (SCP 대비)
- next: kb10 16.2.10 / SCP 16.2.1 (패치 차이, 호환)
- react: 둘 다 19.2.4
- next-intl: kb10 4.13.1 / SCP 4.9.0 (마이너 차이, 호환)

## 미완료·후속 과제
- hreflang 태그 삽입 (다국어 SEO 핵심, DEC-009 후속)
- Phase 3: Vercel 연결 + 가비아 DNS(kbeauty10.com) + Supabase 환경변수 → Supabase 접근정보(URL, anon key, 읽기전용 RLS) 필요
- 첫 파일럿 페이지 /rejuran-gangnam/ 제작

## 교훈 (재발 방지)
- **kb10/kb10_pub 전용 코드스페이스를 따로 열지 말 것.** seoulcp 코드스페이스 하나에서 /workspaces/ 아래 모든 저장소를 오가며 작업 (DEC-008)
- 빈 저장소용 전용 코드스페이스를 열면 README가 자동 생성·커밋되어 로컬 커밋과 충돌(push rejected) 발생. 실제 발생 후 force push로 해결함
- 전용 코드스페이스는 seoulcp 경로가 없어 SCP 참조 명령이 멈춤
