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

---

## 추가 기록 (2026-07-10) — www 연결 완료 + DNS 권장값 갱신

### www 서브도메인 SSL 문제 해결
- 원인: www.kbeauty10.com이 Vercel 프로젝트에 미등록 상태여서 SSL 인증서가 발급되지 않음 (apex만 등록되어 있었음). 20시간 경과에도 자동 해결 안 됨
- 조치: Vercel kb10 프로젝트 Domains에 www.kbeauty10.com 추가 → SSL 인증서 발급 시작 및 완료
- 결과: https://www.kbeauty10.com 정상 (자물쇠 O), apex(kbeauty10.com)로 308 리다이렉트

### 도메인 구조 확정 (apex 메인)
- kbeauty10.com → 실제 사이트 표시 (Connect to environment, Production)
- www.kbeauty10.com → kbeauty10.com으로 308 리다이렉트
- 검증: kbeauty10.com 입력 시 www로 튕기지 않고 /en 유지 O / www 입력 시 apex로 이동 O

### DNS 권장값 갱신 (Vercel IP 대역 확장 대응)
- A 레코드(apex): 76.76.21.21 → 216.198.79.1 로 변경 완료
- CNAME 레코드(www): cname.vercel-dns.com. → 28637ee1505ec1b8.vercel-dns-017.com. 로 변경 완료
- 네임서버: 가비아 기본값(ns.gabia.co.kr) 유지

### 가비아 소유자 정보
- 도메인 소유자명 오타 발견. 가비아 소유자정보 화면에서는 이름 필드가 비활성(수정 불가)
- 조치: 가비아에 소유자명 오타 수정 요청 접수 (처리 대기 중). 사이트 운영/배포에는 영향 없음

### 교훈
- apex 도메인만 추가하면 www는 자동 연결 안 됨. www 서브도메인은 Vercel에 별도 등록 필수
- Vercel 도메인 상태의 "DNS Change Recommended"는 IP 대역 확장 안내. 기존 값도 작동하나 새 값 적용 권장. CNAME 새 값은 도메인별 고유값이므로 화면에서 복사해 사용
- 도메인 등록자(소유자) 이름은 연락처 정보와 달리 일반 수정 화면에서 변경 불가. 등록기관(가비아)을 통한 별도 절차 필요
