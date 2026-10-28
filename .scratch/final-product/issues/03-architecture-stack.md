# 03: 아키텍처와 스택

Type: grilling
Status: open
Blocked by: 02, 10

## Question

본선 제품의 앱 구성(앱 개수), 웹 스택(HTMX + JSON API 유지 또는 Next.js), 화면별 렌더링(공개 목록 SSR + CDN 캐시, 담당자 화면 PWA 여부), 저장소 구조는 무엇인가? 웹 화면은 SaaS 레이아웃과 블로그 디자인 시스템을, 휴대폰 화면은 성은님 목업의 동작과 스타일을 보존해야 한다.

배정 CSP(티켓 10)가 NHN Cloud 이면 서버, PostgreSQL, Object Storage, CDN 을 NHN Cloud 상품으로 매핑하는 것도 이 티켓에서 정한다.
