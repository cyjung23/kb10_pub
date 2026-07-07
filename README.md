# kbeauty10 (kb10) 표준문서

K-beauty 미용의료 정보를 외국인 관광객에게 제공하는 큐레이션 웹서비스의 프로젝트 문서 저장소.

- 서비스: https://kbeauty10.com
- 기술스택: Next.js, next-intl, Supabase, Vercel
- 타겟: 한국 미용의료(피부과 중심)에 관심 있는 외국인 관광객
- 지원 언어: English(기본), 한국어
- 성격: 무대가·무중계 순수 정보 제공 (SCP와 동일 원칙 승계)

---

## 저장소 이원화

| 저장소 | 공개 | 내용 |
|--------|------|------|
| `cyjung23/kb10` | Private | 서비스 소스코드 |
| `cyjung23/kb10_pub` | Public | 표준문서(docs/) + README.md |

표준문서는 `kb10_pub`에만 저장한다. `kb10`에 표준문서를 두지 않는다.

---

## 작업 환경

seoulcp Codespaces 터미널에서 작업. `/workspaces/` 아래 kb10 계열이 클론되어 있다.

- `/workspaces/kb10/` — 소스코드 (Private)
- `/workspaces/kb10_pub/` — 표준문서 (Public)

---

## AI가 지켜야 할 규칙

1. **파일 생성/수정은 heredoc 명령으로만 제공**: `cat > /workspaces/kb10_pub/docs/... << 'EOF' ... EOF` 형식. 사용자는 터미널에 붙여넣기만 한다.
2. **파일 경로는 항상 절대경로 사용**: `/workspaces/kb10/...` 또는 `/workspaces/kb10_pub/...` 형식. 단, git 명령만 해당 저장소로 cd 이동 후 실행.
3. **긴 파일 수정 시 3단계 안전 방식**: 원본을 `/tmp/`에 백업 → 임시 블록 생성 → `head`+`cat`+`tail`로 재조립.
4. **git 명령은 파일 작업과 분리해 별도 제공**: 파일 생성/수정 → 사용자 확인 → 그다음 git add/commit/push 안내.

---

## 핵심 원칙 (법적 기준선, SCP에서 승계)

- 병원으로부터 금전 미수취 (무대가)
- 예약·상담·송객 기능 없음 (무중계)
- 순위·비교·과장·전후사진·후기 배제 (중립 표현)
- SCP DB 원문은 반드시 리라이팅 (중복 콘텐츠 회피)

---

## 문서 구조

| 폴더 | 내용 |
|------|------|
| s1-master/ | 프로젝트 개요, 정체성, 기술 스택 |
| s2-data/ | 데이터 현황, changelog |
| s3-completed/ | 완료 작업 이력 |
| s4-active/ | 진행/보류 작업, 우선순위 |
| s5-decisions/ | 의사결정 로그 (DEC-001~) |
| s6-roadmap/ | 로드맵, 마일스톤 |

---

*최초 생성: 2026-07-07*
