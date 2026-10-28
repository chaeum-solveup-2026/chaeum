# 17: NCP API 키 없이 인프라를 코드로 관리하는 방법

Type: grilling
Status: resolved
Blocked by: None (can start immediately)

## Question

플랫폼 발급 NCP 계정에서 API 인증키에 접근할 수 없다(15). "클라우드 자원은 코드로 관리한다"는 원칙을 어떻게 지킬 것인가? 후보: (a) 사무국에 테라폼용 인증키 발급 요청, (b) NCP 자원은 콘솔로 만들되 구성을 문서와 테라폼 import 가능한 형태로 기록하고, 서버 안 구성(docker compose, GoCD, 런타임 설정)은 Ansible 이나 cloud-init 같은 SSH 기반 코드로 관리, DNS 는 cloudflare 테라폼, (c) 인증키를 쓸 수 있는 다른 계정. 비용, 대표자 1인 접속 제약, 심사에서의 설명 가능성을 함께 따진다. ADR 0003 을 이 결정에 맞춰 고친다.

## Answer

2026-10-28 찬규님 결정: (b).

- NCP 자원은 테라폼 코드(ncloud provider)로 먼저 작성해 저장소에 둔다. 이 코드가 구성의 기준이다
- 콘솔에서는 그 코드 그대로 자원을 직접 만든다(대표자 1인 접속). 코드와 콘솔이 어긋나지 않게, 만든 뒤 콘솔 값을 코드와 대조한다
- API 키가 없어 plan 과 apply 는 못 하므로, 코드는 fmt 와 validate 까지만 자동 검사한다. 나중에 키를 받으면 terraform import 로 콘솔 자원을 상태에 가져와 그때부터 apply 로 관리한다
- 서버 안 구성(docker compose, GoCD, 런타임 설정)은 SSH 기반 코드(Ansible 또는 cloud-init)로 관리하고, DNS 는 cloudflare 테라폼으로 실제 apply 한다
- 사무국에 테라폼용 인증키 발급을 문의하는 것은 막지 않는다(되면 import 로 전환)
