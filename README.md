# 채움

채움은 재난 현장의 부족 품목을 기존 구호 체계에 잇는 연계 서비스다. 담당자가 이미 쓰는 엑셀과 단체 대화방 문장을 대피소별 부족 목록으로 바꾸고, 그 목록을 기부자와 기존 모금 창구에 공개 API와 위젯으로 공급한다.

2026 AI-디지털 기반 사회문제 해결 챌린지 출품작이다.

## 현재 상태

이 저장소는 본선에서 개발할 제품의 저장소다. 예선 상세기획서를 제출하는 시점에는 계획과 설계 결정 기록이 올라와 있고, 서비스 코드는 아직 없다. 코드는 일정표에 따라 올라온다.

| 있는 것 | 위치 |
|---|---|
| 본선 계획 지도와 결정 기록 17건 | [docs/planning/final-product/](docs/planning/final-product/) |
| 설계 결정 기록(ADR) | [docs/adr/](docs/adr/) |
| 용어집 | [GLOSSARY.md](GLOSSARY.md) |
| 개발 티켓 34건과 주 단위 마일스톤 | [Issues](https://github.com/chaeum-solveup-2026/chaeum/issues), [Milestones](https://github.com/chaeum-solveup-2026/chaeum/milestones) |

진행 상황은 Issues와 Milestones에서 볼 수 있다. 예선 단계에서 만든 시연용 구현(PoC)은 별도 저장소에서 개발했고, 그 시연 영상은 상세기획서의 붙임 파일로 제출했다.

## 왜 만드는가

재난이 나면 시민과 기업의 선의는 넘치지만, 현장에 지금 무엇이 얼마나 부족한지는 보이지 않는다. 담당자는 요청을 전화, 엑셀, 단체 대화방으로 주고받고, 기부자는 추측으로 물품을 보낸다. 그 결과 쓰지 못하고 버려지는 구호품이 생긴다. 2025년 경북 산불에서는 쓰지 못하고 버려진 구호품이 11톤이었고, 2019년 강원 산불에서는 들어온 헌 옷 53톤 중 30톤이 폐기되었다. 출처는 상세기획서에 있다.

## 본선에서 만들 것

범위는 [기능 범위 결정](docs/planning/final-product/issues/02-feature-scope.md)에 있다.

- 엑셀 업로드와 열 매핑, 문장 붙여넣기, 문자 형식 해석
- 해석 결과의 자동 반영, 확인 권장, 확인 필수 구분
- 배정, 배송 중, 수령 확인, 기부 전 확인과 조건부 배정
- 공개 목록과 공개 API, 모금 페이지 위젯, 엑셀 내보내기
- 현황판과 대피소 지도
- PWA 오프라인 기록과 동기화
- 평시 모드(폭염, 한파 물품 배분)
- 현장 경험자 5명 이상의 사용성 테스트(SUS)

## 기술 구성

- 웹은 Next.js, API는 Spring Boot이며 컨테이너 2개로 배포한다. 데이터베이스는 PostgreSQL이다.
- 배포는 네이버 클라우드 플랫폼(NCP)의 서버 1대와 관리형 DB, CDN이다. 자원은 테라폼 코드를 기준으로 작성한다.
- 빌드와 배포는 GitHub Actions와 NCP 자체 실행기로 한다.

결정의 이유와 대안은 [docs/adr/](docs/adr/)와 [아키텍처 결정](docs/planning/final-product/issues/03-architecture-stack.md)에 있다.

## 일정

| 기간 | 내용 |
|---|---|
| 10/26(월) ~ 11/03(화) | 본선 진출 통보 전. 개발 환경 뼈대(Next.js, Spring Boot, PostgreSQL, docker compose, CI), 대피소 API 이용신청 |
| 11/04(수) ~ 11/08(일) | NCP 인프라 코드와 첫 배포, 해석기 이식, 협력 기관 접촉, 가상 데이터 |
| 11/09(월) ~ 11/15(일) | 담당자 로그인, 문장과 엑셀 입력에서 공개 목록까지 첫 배포(tracer bullet), 정답 표 검수 |
| 11/16(월) ~ 11/22(일) | 수령 확인, 배정과 기부 전 확인, 현황판과 지도, 모금 페이지 위젯 |
| 11/23(월) ~ 11/29(일) | 오프라인 기록, 문자 형식, 평시 모드, 랜딩, 사용성 테스트 |
| 11/30(월) ~ | 발표 준비(분류 모델은 여유가 있을 때) |

일정은 본선 진출 통보일에 따라 달라질 수 있다. 세부 일정과 늦어질 때 빼는 순서는 [일정과 역할 결정](docs/planning/final-product/issues/09-schedule-roles.md)에 있다.

## 읽는 순서

1. [GLOSSARY.md](GLOSSARY.md): 이 저장소가 쓰는 용어
2. [docs/planning/final-product/map.md](docs/planning/final-product/map.md): 본선 계획의 결정 요약
3. [docs/adr/](docs/adr/): 설계 결정과 그 이유
4. [Issues](https://github.com/chaeum-solveup-2026/chaeum/issues): 개발 티켓
