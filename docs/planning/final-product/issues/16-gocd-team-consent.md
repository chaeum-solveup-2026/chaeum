# 16: CI/CD 도구 선택(GoCD 보류)

Type: grilling
Status: resolved
Blocked by: None (can start immediately)

## Question

CI/CD 와 배치 흐름을 GoCD 한 곳에서 보는 안(ADR 0004)을 지금 채택할 것인가? 채택하지 않으면 GitHub Actions(+ NCP 자체 실행기)로 가고 배치는 앱 안 스케줄로 돌린다.

## Answer

- (2026-10-28) GoCD 는 지금 채택하지 않고 보류한다.
- 티켓에 정해 둔 대안으로 간다: CI/CD 는 GitHub Actions(실행 시간 제한에 대비해 NCP 서버의 자체 실행기 사용), 대피소 데이터 수집은 앱 안 스케줄. 배포는 그대로 서버 1대 docker compose.
- GoCD 는 제품으로 가치를 보인 뒤 다시 검토한다. 그때까지 MVP 뒤 여유 목록(k3s, Argo CD 와 같은 자리)에 둔다.
