# GS E&C Modularization Portal

GS E&C 사내 참조용 Modularization 통합 대시보드 프로젝트. 정적 HTML 5개 파일을 GitHub Pages에 배포하여 운영.

## 📁 프로젝트 구조

```
참조 Modularization 자료/
├── index.html                                  # 🏠 포털 랜딩 (4개 카드)
├── Modularization_RnR_ITC_by_Discipline.html   # 📊 R&R 대시보드 (Page 1/2/3 + SPMT 시뮬레이션)
├── Module 적용 절차 초안.html                  # 📋 절차 가이드 (Tailwind + Chart.js)
├── lessons_learned_dashboard.html              # 📈 Lessons Learned (MFC)
├── Module_Work_Flow_Ontology.html              # 🗂️ MFC PAR Module 백서
├── folder_data.js                              # 백서 의존 데이터 (304KB)
├── Modularization_Flow.png                     # 로그인/포털 배경
├── module_transport_bg.png                     # SPMT 애니메이션 배경
├── 모듈조직도_As_Is_But.png                    # 조직도 (현재)
├── 모듈조직도_future_O.png                     # 조직도 (미래)
├── secure/                                     # 🔐 StatiCrypt AES-256 암호화 버전
│   └── (위와 동일 구성, 4개 HTML이 암호화됨)
└── .claude/
    └── launch.json                             # 정적 서버 설정 (npx http-server)
```

## 🔑 인증 정보

| 위치 | ID | Password |
|------|----|----|
| **포털 로그인** (index.html) | `RayHan` | `Modularization` |
| **서브페이지 로그인** (4개 대시보드) | `ModuleSolution` | `Modularization2` |
| **StatiCrypt 복호화** (secure/ 전용) | — | `Modularization2` |

### 인증 구현 방식
- **방식**: Web Crypto API SHA-256 해시 비교
- **저장**: `sessionStorage.setItem('mod-rnr-auth', 'ok')`
- **포털 해시**: `c4dc3fe9c9fe8173c7645fed9f4f83f7f1a37fced165830e1bf2690c044b2f38` (RayHan:Modularization)
- **서브 해시**: `1ba7e9226fa19275af643dfadff5bc7f0740692f9c4d24ce3a617fdc794b2f37` (ModuleSolution:Modularization2)
- **세션 가드**: 모든 서브페이지 `<head>` 첫줄에 `if(sessionStorage.getItem('mod-rnr-auth')!=='ok')window.location.href='index.html'`

## 🚀 배포

- **Git 리포지토리**: https://github.com/lRayHanl/modularization-rnr-dashboard
- **GitHub Pages**:
  - 원본: https://lrayhanl.github.io/modularization-rnr-dashboard/
  - 암호화: https://lrayhanl.github.io/modularization-rnr-dashboard/secure/
- **로컬 경로**: `E:\공유폴더\CoworkProjects\참조 Modularization 자료\`
- **브랜치**: `main`

## 🔒 보호 기능

### 1. JS 복사 방지 (모든 5개 HTML 파일)
- `copy`/`cut`/`paste` 이벤트 차단 (capture phase)
- `clipboardData.setData('text/plain','')` 으로 클립보드 비우기
- `user-select: none !important` (CSS)
- 우클릭, 드래그, F12, Ctrl+C/X/A/S/P/U, Ctrl+Shift+I/J/C 차단
- `@media print { body > * { display: none !important; } }` 인쇄 차단
- `<input>`/`<textarea>` 안에서는 입력 허용 (로그인 필드용)

### 2. StatiCrypt AES-256 암호화 (`/secure/`)
- 도구: `npx staticrypt` (https://github.com/robinmoisson/staticrypt)
- 비밀번호: `Modularization2`
- 효과: Network 탭 다운로드 시 암호문만 보임, View Source도 암호문
- 한계: 렌더링 후 DOM은 메모리에 평문 존재 (F12로 확인 가능)

## 📝 주요 작업 이력

| 단계 | 내용 |
|------|------|
| Phase 1-2 | PDF/Excel 소스 → 인터랙티브 HTML 매트릭스 변환 |
| Phase 3 | Page 3 SPMT 워크플로우 시뮬레이션 (SVG snake timeline, Barge, 노드 드래그) |
| Phase 4 | Page 1/2 KPI 카드 + 도넛 차트 |
| Phase 5 | GitHub Pages 배포 + SHA-256 인증 게이트 |
| Phase 6 | 손그림 SVG 조직도 → PNG 이미지 교체 |
| Phase 7 | 포털 랜딩 (`index.html`) 통합 — 4개 카드 |
| Phase 8 | 인증정보 변경: RayHan/Modularization, ModuleSolution/Modularization2 |
| Phase 9 | `Modularization_Flow.png` 배경 적용 (로그인 반투명, 포털 불투명) |
| Phase 10 | 복사 방지 강화 (`copy` 이벤트 직접 차단) |
| Phase 11 | StatiCrypt 암호화 버전 `/secure/` 추가 |

## 🛠 개발 환경

- **OS**: Windows
- **Node**: v24.14.1, npm 11.11.0
- **Git**: UTF-8 한글 폴더명 지원
- **로컬 서버**: `npx http-server . -p 8080` (정적 파일)
- **빌드 도구 없음**: 순수 HTML/CSS/JS
- **CDN 의존**: Tailwind CSS (절차 페이지), Chart.js, Modularization_Flow.png

## ⚠️ 주의사항

### 파일 작업
- HTML 파일 한글 파일명 (예: `Module 적용 절차 초안.html`) — Bash에서 따옴표 필수
- `Edit` 도구로 수정 후 secure/ 버전 재암호화 필요시:
  ```bash
  npx --yes staticrypt "<filename>" -p "Modularization2" -d "secure" --short
  ```

### 인증 게이트 수정 시
- 모든 서브페이지에 동일한 sessionStorage 키 (`mod-rnr-auth`) 사용
- 해시 변경 시 모든 페이지의 `_SUB_HASH` 또는 `AUTH_HASHES` 동기화 필요

### Page 3 SPMT 시뮬레이션 (대시보드)
- SVG `offset-path` CSS 애니메이션 사용
- `window.SPMT_NODES`, `window.SPMT_SEGS` 글로벌 데이터
- 노드 좌표 클램프: `x ∈ [55, 1345], y ∈ [65, 775]`
- Barge 활성화는 시간% 기준 (거리% 아님) — 노드 60-62 구간

### Git
- 라인 엔딩 경고 (LF → CRLF) 무시 가능
- 대용량 파일: `lessons_learned_dashboard.html` 23MB (이미지 임베드)
- `.gitignore`의 `[brackets]` 패턴은 glob으로 해석되므로 이스케이프 필요

## 🎯 자주 요청되는 작업 패턴

1. **인증정보 변경**: SHA-256 해시 재계산 → 모든 페이지의 hash 변수 업데이트
2. **새 페이지 추가**: index.html 카드 추가 + 세션가드 + 서브 인증게이트 + 복사방지 스크립트
3. **복사방지 강화**: `</body>` 직전에 protection script 블록 추가
4. **암호화 버전 갱신**: 원본 수정 → secure/에서 해당 파일 삭제 → staticrypt 재실행 → commit/push

## 📚 참고

- 원래 사용자: oilandgas@gsenc.com (GS E&C)
- GitHub 계정: `lRayHanl` (대문자 H — 케이스 주의)
- 프로젝트는 사내 참조용이며 외부 배포 금지 표기됨
