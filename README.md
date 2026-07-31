# 리메인솔라 플랫폼

인삼밭의 생육 환경과 태양광 발전을 함께 최적화하는 AI 기반 접이식 영농형 태양광 플랫폼입니다. 사업계획서의 MVP 범위와 DESIGN-stripe.md의 디자인 언어를 실제 반응형 제품 UI로 구현했습니다.

## 주요 기능

- 브랜드 랜딩 및 플랫폼 소개
- 실시간 발전·생육·수익 대시보드 데모
- 차양 개방률 제어 인터랙션과 성공 알림
- 실증 상담 폼 검증 및 API 저장
- 관리자 로그인, 목록·필터, 상태 변경, 상세 Drawer, 삭제
- D1 배포 API + Express/SQLite 로컬 백엔드 샘플
- Figma 구조, 디자인 토큰, 컴포넌트 매핑, 개발자 핸드오프

## 기술 스택

- Web: Next-compatible Vinext, React 19, TypeScript, CSS
- Hosted API/DB: Cloudflare Worker + D1
- Local backend: Node.js + Express + SQLite(better-sqlite3)
- Hosting: OpenAI Sites

## 구조

~~~text
app/
  page.tsx
  ui/MarketingHome.tsx
  dashboard/
  admin/
  api/
backend/
  server.js
  database.js
  routes/
db/schema.ts
docs/platform-plan.md
figma-guide/
  figma-structure.md
  design-tokens.json
  component-mapping.md
  developer-handoff.md
public/og.png
~~~

## 웹사이트 실행

Node.js 22 이상을 권장합니다.

~~~bash
npm install
npm run dev
~~~

브라우저에서 표시된 Local URL에 접속합니다. 메인은 /, 운영 콘솔은 /dashboard, 관리자는 /admin 입니다.

## Express + SQLite 백엔드만 실행

~~~bash
cd backend
npm install
npm start
~~~

API 기본 주소는 http://localhost:4000 입니다. 프론트와 분리 실행할 때는 프론트 API base URL을 이 주소로 변경하세요.

## 관리자 테스트 계정

- ID: admin
- Password: admin1234

## API

| Method | Endpoint | 기능 |
|---|---|---|
| POST | /api/applications | 실증·문의 저장 |
| GET | /api/applications | 관리자 목록 |
| PATCH | /api/applications/:id | 상태 변경 |
| DELETE | /api/applications/:id | 삭제 |
| POST | /api/admin/login | 관리자 로그인 |

## 반응형 기준

- Mobile: 320–767px, 1열·햄버거·전체 너비 CTA
- Tablet: 768–1023px, 2열 중심
- Desktop: 1024px+, 사이드바·복합 패널
- Wide: 1440px+, 1280px 콘텐츠 확장

## Figma 수정

figma-guide/figma-structure.md의 Page/Frame 구조로 화면을 옮기고, 색·간격은 figma-guide/design-tokens.json을 Variable로 등록합니다. 수정 후 app/globals.css의 동일 의미 CSS 변수를 변경하면 전체 화면에 반영됩니다.

## 보안 안내

현재 로그인은 로컬 MVP 검증용입니다. 실제 서비스에서는 비밀번호 해싱(Argon2/bcrypt), 환경변수·secret 관리, 만료되는 서버 세션 또는 JWT, HTTPS, CSRF 방지, 요청 속도 제한, 감사 로그, 개인정보 암호화·보유기간 정책, 역할 기반 권한을 반드시 적용해야 합니다.

## 향후 확장

농가 계정·마이페이지, 실제 IoT 제어, 기상 API, AI 발전량 예측, 리포트 PDF, 알림, 파일 업로드, 검색·필터, 유지보수 티켓, 결제·구독을 독립 라우터와 컴포넌트로 추가할 수 있습니다.
