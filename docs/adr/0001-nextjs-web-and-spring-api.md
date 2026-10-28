# 웹은 Next.js, 백엔드는 Spring Boot JSON API, 같은 서버의 컨테이너 2개

예선 PoC 는 Spring Boot 앱 하나가 HTMX 화면과 JSON API 를 함께 냈다. 본선 제품은 클라우드 자원에 여유가 있고 상세기획서도 Next.js 를 적었으므로, 화면은 모두 Next.js(공개 목록과 랜딩은 서버 렌더링 + CDN 30초 HTTP 캐시, 담당자 화면은 PWA)가 맡고 Spring Boot 는 JSON REST API 만 낸다. 해석기를 Kotlin 그대로 옮기기 위해 백엔드는 Spring Boot 를 유지한다. 두 컨테이너는 같은 NCP 서버에서 돌고 Load Balancer 가 /api 를 Spring 으로, 나머지를 Next.js 로 보내 같은 도메인에서 쿠키 인증을 쓴다. HTMX 템플릿은 가져오지 않는다.
