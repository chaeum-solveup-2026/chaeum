# NCP 서버 1대 + 관리형 DB + CDN, 클라우드 자원은 테라폼 코드를 기준으로 만든다

본선 제품은 3주, 2명이 만든다. 쿠버네티스(관리형 NKS 또는 서버에 직접 올린 k3s)와 Argo CD 는 운영과 구성 부담이 커서 MVP 뒤 여유가 있을 때로 미루고, 앱 컨테이너 2개를 NCP 서버(VPC) 1대의 docker compose 로 돌린다. DB 는 Cloud DB for PostgreSQL(핵심은 테이블, 모양이 제각각인 원본은 JSONB), 엑셀 원본은 Object Storage, 공개 페이지와 공개 API 앞에는 CDN 을 둔다.

민관협력 지원 플랫폼이 발급한 NCP 계정에서는 API 인증키에 접근할 수 없어 테라폼으로 NCP 자원을 직접 만들 수 없다. 그래서 NCP 자원은 테라폼 코드(ncloud provider)로 먼저 작성해 구성의 기준으로 삼고, 콘솔에서 그 코드대로 직접 만든 뒤 값을 대조한다. 코드는 fmt 와 validate 까지만 자동 검사하고, 인증키를 받게 되면 terraform import 로 상태를 가져와 apply 로 전환한다. 서버 안 구성은 Ansible 이나 cloud-init 으로, DNS 는 cloudflare 테라폼으로 실제 적용한다. 인증키와 state 는 저장소에 두지 않는다.
