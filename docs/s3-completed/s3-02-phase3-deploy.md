# Phase 3 완료 기록 — Vercel 배포 + 도메인 연결

완료일: 2026-07-09

## 작업 요약
- Vercel에 kb10(Private) 저장소 임포트 및 배포 (커밋 b8c536d, 상태 Ready)
- 기본 배포 주소: kb10.vercel.app (Valid Configuration)
- 커스텀 도메인 kbeauty10.com 연결 (apex 도메인, Production 환경)
- apex 도메인 우선 정책 유지: "Redirect apex to www" 체크 해제

## 가비아 DNS 설정
- A 레코드: 호스트 @, 값 76.76.21.21, TTL 600
- CNAME 레코드: 호스트 www, 값 cname.vercel-dns.com., TTL 3600
- 네임서버: 가비아 기본값(ns.gabia.co.kr) 유지, 위임 변경 없음

## 검증 결과
- https://kbeauty10.com → 정상 (SSL 자물쇠 O, /en 자동 리다이렉트, "K-beauty in Seoul" 페이지 표시)
- https://www.kbeauty10.com → www용 SSL 인증서 발급 지연으로 일시 경고(NET::ERR_CERT_COMMON_NAME_INVALID). 시간 경과 후 자동 해결 예정
- DNS 전파는 TTL 600 덕분에 Refresh 없이 자동 반영됨

## 미결/후속 확인
- www 서브도메인 SSL 인증서 발급 완료 여부 재확인 (30분~수시간 내 자동)
- Vercel "DNS Change Recommended"(노란 배지) 검토 — A 레코드 방식은 정상 작동 중이므로 급하지 않음. 초기 단계에서는 현행 유지
- hreflang 태그 삽입 (다국어 SEO, DEC-009 후속)
- Phase 4: Supabase 환경변수 등록(URL, anon key, 읽기전용 RLS) 및 첫 파일럿 페이지 /rejuran-gangnam/ 제작

## 교훈
- apex는 SSL 먼저, www(CNAME)는 인증서 발급이 뒤늦게 진행됨. www 접속 시 일시적 인증서 경고는 정상 과정이며 대기하면 해소됨
- 인증서 경고 화면에서 "고급→접속"으로 강제 진입하지 말 것
