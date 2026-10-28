# 04: NCP 배포 구성과 승인 상태

Type: research
Status: resolved
Blocked by: None (can start immediately)

## Question

민관협력 지원 플랫폼의 NCP 계정 승인 상태와 사용 범위는? 본선 제품을 배포하는 데 필요한 NCP 상품(서버 또는 컨테이너, Cloud DB for PostgreSQL, Object Storage, Load Balancer, CDN), 제약(팀당 CSP 계정 1개, 비용 무상 범위, AI 상품 금지 규정), 배포 절차는 무엇인가?

## Answer

조사 브랜치 research/ncp-deploy (커밋 c52a989, 문서 docs/research/ncp-deploy.md, worktree ../chaeum-research-ncp).

- (사실) 연결 가능한 민간 클라우드는 NCP, KT Cloud, NHN Cloud 세 곳이나, 운영 사무국 GitBook 안내(cccr.gitbook.io/2025-doc)에 2026년 7월 기준 NCP 와 KT Cloud 는 자원 소진으로 신규 발급 중단, NHN Cloud 만 신규 발급 가능하다고 적혀 있다. "NCP 배포" 전제가 성립하지 않을 수 있다.
- (사실) 10/22 사무국에 사용 신청, 같은 날 절차 안내 메일 수신. 채움 팀을 특정한 승인 확인 메일은 찾지 못했다.
- (사실) 팀당 CSP 계정 1개, 대표자만 콘솔 접속(다른 팀원이 접속하면 그 시점에 계정 발급), 예선 탈락 시 회수, 수상자는 2027-12 까지 연장.
- (사실) 민간 클라우드를 통한 AI 기능은 비용 문제로 사용 금지.
- (사실, 부분) 플랫폼 계정 경유 접속만 비용 지원, 사용량 한도 초과 시 일시정지 가능. 구체 한도는 비공개.
- (사실) 절차: 플랫폼 사용 신청 -> 사무국 승인 -> 디지털 자원 카탈로그의 클라우드에서 CSP 콘솔 진입.
- (추정) NCP 상품별 사양과 무상 한도는 확인하지 못했다. NCP 가 막혀 있으면 의미가 줄어 우선순위를 낮췄다.

후속: 실제 배정된 CSP 확인은 사람만 할 수 있어 티켓 10 으로 분리한다. CSP 에 따른 리소스 매핑은 티켓 03 의 질문에 포함한다.
