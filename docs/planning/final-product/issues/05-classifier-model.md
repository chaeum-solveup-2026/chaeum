# 05: 분류 모델(C안)을 실제로 넣을지

Type: research
Status: resolved
Blocked by: None (can start immediately)

## Question

laya(mmBERT 기반, 약 647MB) 분류 모델을 ONNX 로 변환해 JVM 에서 CPU 추론할 수 있는가? 메모리, 지연, 대안(더 작은 모델, Python 사이드카, 규칙 파서만 유지)은? 활용성 점수에 주는 효과 대비 비용은?

## Answer

조사 브랜치 research/classifier-model (커밋 5f6a6b7, 문서 docs/research/classifier-model.md, worktree ../chaeum-research-classifier).

- (사실) laya(HF 2nugu/laya-ko)는 mmBERT-base(322M) 기반, fp16 가중치 644MB. 저장소에 fp32 ONNX(opset 20, 1.29GB)가 이미 공개되어 있어 변환은 끝나 있다.
- (사실) ModernBERT 계열이라 optimum ONNX 재변환이 실패한 사례가 여럿 보고됐다. 재변환이 필요해지면 위험이 있다.
- (사실) JVM 에서는 ONNX Runtime Java 또는 DJL 로 CPU 추론할 수 있다(네이티브 메모리).
- (추정) fp32 그대로면 상주 메모리 2~2.5GB. CPU 지연은 전용 벤치마크가 없어 실측 전까지 모른다. 참고로 빅콘테스트의 Python 사이드카 시험은 요청 1건당 약 0.45~0.5초였다(다른 분류 기준이라 F1 근거로는 못 씀).
- (권고) JVM 에 laya 를 직접 넣는 것은 1순위가 아니다. 순서: 규칙 파서 오류를 사전, 규칙 보강으로 먼저 줄이기 -> 필요하면 표준 BERT 계열 소형 모델(MiniLM, XLM-R base) ONNX -> laya 정밀도가 꼭 필요하면 Python 사이드카로 분리.
- (확인 불가) 이 결정의 가치는 배점과 라벨 데이터셋 유무에 달려 있다. 본선 배점에는 "활용성" 항목이 없고(완성도, 확장성, 유용성, 기획성, 발표), AI 활용은 예선 활용성(20점)에서만 직접 평가됐다.

후속: 분류 모델을 본선 제품에 넣을지는 기능 범위(02)에서 정한다. 넣는다면 라벨 데이터셋 확보, 모델 크기(fp16, int8, 소형 모델), 사이드카 여부를 아키텍처(03)에서 정한다.
