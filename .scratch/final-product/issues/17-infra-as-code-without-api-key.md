# 17: NCP API 키 없이 인프라를 코드로 관리하는 방법

Type: grilling
Status: open
Blocked by: None (can start immediately)

## Question

플랫폼 발급 NCP 계정에서 API 인증키에 접근할 수 없다(15). "클라우드 자원은 코드로 관리한다"는 원칙을 어떻게 지킬 것인가? 후보: (a) 사무국에 테라폼용 인증키 발급 요청, (b) NCP 자원은 콘솔로 만들되 구성을 문서와 테라폼 import 가능한 형태로 기록하고, 서버 안 구성(docker compose, GoCD, 런타임 설정)은 Ansible 이나 cloud-init 같은 SSH 기반 코드로 관리, DNS 는 cloudflare 테라폼, (c) 인증키를 쓸 수 있는 다른 계정. 비용, 대표자 1인 접속 제약, 심사에서의 설명 가능성을 함께 따진다. ADR 0003 을 이 결정에 맞춰 고친다.
