# chaeum

채움(2026 AI, 디지털 기반 사회문제 해결 챌린지) 본선 제품 저장소. 예선 PoC 는 `chaeum-solveup-2026/chaeum-poc` 이고, 이 저장소는 그 교훈을 바탕으로 처음부터 다시 만든다. 본선 계획 지도는 `.scratch/final-product/map.md`.

## Agent skills

### Issue tracker

로컬 마크다운. 이슈와 스펙은 `.scratch/<feature>/` 아래 파일로 둔다. 팀원이 공유 저장소 접근을 확인하면 GitHub Issues 로 옮긴다. See `docs/agents/issue-tracker.md`.

### Triage labels

기본 5종(needs-triage, needs-info, ready-for-agent, ready-for-human, wontfix)을 그대로 쓴다. See `docs/agents/triage-labels.md`.

### Domain docs

single-context: 루트 `GLOSSARY.md` + `docs/adr/`. See `docs/agents/domain.md`.
