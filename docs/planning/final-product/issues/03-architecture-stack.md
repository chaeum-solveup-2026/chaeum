# 03: 아키텍처와 스택

Type: grilling
Status: resolved
Blocked by: 02, 10, 13

## Question

본선 제품의 앱 구성(앱 개수), 웹 스택(HTMX + JSON API 유지 또는 Next.js), 화면별 렌더링(공개 목록 SSR + CDN 캐시, 담당자 화면 PWA 여부), 저장소 구조는 무엇인가? 웹 화면은 SaaS 레이아웃과 블로그 디자인 시스템을, 휴대폰 화면은 성은님 목업의 동작과 스타일을 보존해야 한다.

배정 CSP 는 NCP 로 확정(티켓 10). NCP 상품(서버 또는 컨테이너, Cloud DB for PostgreSQL, Object Storage, CDN) 매핑을 이 티켓에서 정한다.

## Answer

2026-10-28 grilling 으로 결정(찬규님). ADR 은 docs/adr/0001~0004.

- 백엔드: Kotlin + Spring Boot + PostgreSQL. 해석기와 측정 하네스를 테스트와 함께 옮긴다. DB 는 핵심(현장, 품목 줄, 배정, 계정)은 테이블, 모양이 제각각인 원본(해석 결과 상세, 엑셀 원본 행, 15139148 원본 응답, 기부 전 확인 입력)은 JSONB
- 화면: Next.js 프론트엔드가 모든 화면을 맡고 Spring 은 JSON REST API 만. 공개 목록과 랜딩은 서버 렌더링 + CDN 30초 HTTP 캐시, 담당자 화면은 PWA(서비스 워커 + 기기 저장소), 현황판은 서버 렌더링 + 화면 내 갱신. HTMX 는 가져오지 않는다 (ADR 0001)
- 목업 이식: 성은님 목업의 휴대폰 화면 구조와 동작을 React 컴포넌트로 옮기고 색과 글꼴만 디자인 토큰으로. 신뢰도 숫자는 화면에서 뺀다
- 배포: NCP 서버(VPC) 1대 + docker compose(Next, Spring), Cloud DB for PostgreSQL, Object Storage, Load Balancer 와 인증서, CDN. LB 가 /api 는 Spring, 나머지는 Next 로 (ADR 0003)
- 인프라 코드: 테라폼 필수. ncloud provider 와 cloudflare provider(DNS), state 는 NCP Object Storage, 인증키는 환경 변수와 비밀 저장소로만 (ADR 0003). 플랫폼 발급 계정에서 API 인증키 발급이 가능한지는 티켓 15 에서 확인
- 도메인: 찬규님 도메인의 하위 도메인(예: chaeum.chan99k.dev)
- 인증: 담당자는 발급 계정의 아이디와 비밀번호 로그인(CSRF 보호), 자기 현장만 수정. 기부자는 로그인 없음. 회원 가입 없음
- CI/CD 와 배치: GoCD 를 별도 작은 서버에 두고 여러 파이프라인과 배치(대피소 데이터 수집, 시간 트리거)를 value stream map 한 화면에서 본다. 조건부 배정 만료는 앱 안에서. 단, GoCD 채택은 팀원(성은님) 동의 후 확정 (ADR 0004 proposed, 티켓 16)
- 분류 모델(여유가 있을 때): JVM 이 아니라 같은 서버의 Python 사이드카, 규칙 파서가 못 읽은 줄만 질의
- 여유가 있을 때: k3s + Argo CD (GoCD 와의 조합도 그때 검토)
- 공공데이터 수집: 15139148 을 하루 한 번(GoCD 파이프라인이 앱의 수집 작업을 호출, GoCD 미채택 시 앱 안 스케줄)
