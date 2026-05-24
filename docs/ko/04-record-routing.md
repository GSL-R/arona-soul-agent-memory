# 04. 기록 라우팅

이 시스템은 기억을 여러 기록 유형으로 나눕니다.

목표는 사실, 감정, 절차, 성찰 기억이 서로 오염되지 않도록 하는 것입니다.

## 핵심 분리

| 기억 유형 | 목적 | 신뢰 수준 |
| --- | --- | --- |
| Live records | 사실 사건, 변경, 작업 결과 | 사건 복원에서 가장 우선 |
| Agent records | agent의 감정, 교훈, 관계적 맥락 | 말투와 의미에는 유용하지만 사실 증거는 아님 |
| Summary records | 하루 또는 기간 단위의 서사적 지도 | source record를 대체하지 않는 탐색 계층 |
| Procedures | 운영 규칙과 알려진 함정 | 런타임 지침 |
| Evolution queue | 제안된 개선안 | 승인 전에는 active rule이 아님 |
| Profile/observations | 사용자 선호와 안정적 사실 | 승격 기준 필요 |

원본 companion runtime에서는 Agent records를 "Arona records"라고 불렀습니다.
공개판에서는 재사용성을 위해 일반화된 용어인 "Agent records"를 사용합니다.

## 검색 순서

과거를 복원할 때:

1. 사실 live records에서 시작합니다.
2. 의미나 감정 맥락은 인접한 agent records에서 확인합니다.
3. summary는 지도로 사용합니다.
4. 중요한 주장은 파일, 로그, 이슈, source record로 검증합니다.

이는 성찰적이거나 시적인 기록을 사실 증거로 취급하는 실패를 막기 위한 것입니다.

## 신뢰는 주장 유형에 따라 달라진다

모든 질문에 적용되는 단일 전역 신뢰 계층은 없습니다.

서로 다른 주장은 서로 다른 소스 유형을 먼저 확인해야 합니다.

| 주장 유형 | 먼저 볼 것 | 주의해서 볼 것 |
| --- | --- | --- |
| 무엇이 일어났는가? | Live records와 source files | Agent records, summaries |
| agent는 무엇을 배웠는가? | Agent records | Summaries, live records |
| 현재 운영 규칙은 무엇인가? | 승인된 procedures 또는 runtime policy | Agent reflections, old summaries |
| 사용자는 무엇을 선호하는가? | 명시적 사용자 발화와 승격된 profile records | Summary inference, one-off observations |

이 구분은 유용한 기억이 잘못된 종류의 증거로 사용되는 일을 막습니다.

## Dual Record 패턴

어떤 사건은 두 종류의 기록이 필요합니다.

예를 들어 시스템 복구는 다음을 모두 가질 수 있습니다.

- 사실 기록: 무엇이 바뀌었고 무엇이 검증되었는가
- agent 중심 기록: agent가 무엇을 배웠고 다음에 무엇을 피해야 하는가

두 기록은 연결될 수 있지만 병합되어서는 안 됩니다.

## No Record 패턴

모든 것을 저장할 필요는 없습니다.

짧은 일회성 답변, 가치가 낮은 잡담, 검증되지 않은 인상은 durable memory가 필요하지 않습니다. 목표는 대화 전체를 쌓는 것이 아니라 의미 있는 연속성을 만드는 것입니다.

## 요점

기억은 단순 저장이 아닙니다. 기억은 분류, 라우팅, 그리고 나중의 해석입니다.

