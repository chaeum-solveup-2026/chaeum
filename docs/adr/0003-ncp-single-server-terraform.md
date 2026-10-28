# NCP 서버 1대 + 관리형 DB + CDN, 모든 클라우드 자원은 테라폼으로 관리

본선 제품은 3주, 2명이 만든다. 쿠버네티스(관리형 NKS 또는 서버에 직접 올린 k3s)와 Argo CD 는 운영과 구성 부담이 커서 MVP 뒤 여유가 있을 때로 미루고, 앱 컨테이너 2개를 NCP 서버(VPC) 1대의 docker compose 로 돌린다. DB 는 Cloud DB for PostgreSQL(핵심은 테이블, 모양이 제각각인 원본은 JSONB), 엑셀 원본은 Object Storage, 공개 페이지와 공개 API 앞에는 CDN 을 둔다. 모든 NCP 자원과 DNS(Cloudflare)는 테라폼으로 코드화하고, state 는 NCP Object Storage 에 두며 인증키는 환경 변수와 비밀 저장소로만 넘긴다.
