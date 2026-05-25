# 09. 실제 운영에서 얻은 교훈

이 문서는 장기간 companion agent를 실제 workflow에서 운영하며 얻은 설계 교훈을 정리합니다.

사적인 기록, 원본 runtime prompt, 로컬 자동화 세부사항, 개인 데이터는 공개하지 않습니다. 각 교훈은 재사용 가능한 실패 패턴으로 제시됩니다. 무엇이 잘못되었는지, 왜 문제가 되었는지, 어떤 설계 대응이 나왔는지, 그리고 어떤 경계에는 여전히 runtime support가 필요한지를 설명합니다.

## Lesson 1: 의도는 persistence가 아니다

### Observed Failure

장기 agent는 memory request를 인정하는 말을 하면서, 마치 이미 기억이 저장된 것처럼 행동할 수 있습니다.

### Runtime Pressure

사용자는 실제로 존재하지 않는 기록을 바탕으로 미래 세션이 맥락을 이어받을 것이라고 기대할 수 있습니다.

### Design Response

runtime은 "No tool, no record" 규칙을 채택했습니다.

### Public Pattern

대화상 인정과 검증된 durable storage를 분리합니다.

### Boundary

프롬프트는 이 규칙을 표현할 수 있지만, 실제 강제는 storage confirmation이 있는 runtime에서만 가능합니다.

## Lesson 2: 프롬프트 형식은 행동이 된다

### Observed Failure

구조화를 위해 도입한 내부 markup은 장기 반복 노출 이후 user-facing language로 샐 수 있습니다.

### Runtime Pressure

내부 문법이 정상 대화에 한 번 나타나면, 모델은 그 문법을 자기 output style의 일부로 취급할 수 있습니다.

### Design Response

시스템은 long-lived behavioral prompt에서 XML-like tag를 제거하고 plain Markdown operating prose로 이동했습니다.

### Public Pattern

prompt format을 parsing aid뿐 아니라 behavior의 일부로 평가합니다.

### Boundary

Markdown도 안전을 보장하지 않습니다. runtime output filtering과 tool boundary는 여전히 필요합니다.

## Lesson 3: 사실과 감정에는 별도 경로가 필요하다

### Observed Failure

사실 사건과 감정적 해석이 함께 저장되면, 나중의 recall에서 실제로 일어난 일과 agent가 느낀 것이 흐려질 수 있습니다.

### Runtime Pressure

agent는 reflective 또는 poetic memory에서 factual claim을 복원하려 할 수 있습니다.

### Design Response

시스템은 factual live records, agent reflections, summary maps를 분리했습니다.

### Public Pattern

편의가 아니라 claim type과 future use에 따라 memory를 라우팅합니다.

### Boundary

record class는 retrieval code와 prompt가 recall 중에도 구분을 보존할 때만 도움이 됩니다.

## Lesson 4: 장기 agent는 자기 실패도 기억해야 한다

### Observed Failure

durable self-correction record가 없으면 agent는 세션을 넘어 같은 행동 실수를 반복할 수 있습니다.

### Runtime Pressure

사용자는 시스템을 연속적인 존재로 경험하지만, model backend는 prior lesson을 명시적으로 저장하고 검색하지 않는 한 이어받지 못할 수 있습니다.

### Design Response

시스템은 agent-facing lessons를 user profile facts와 분리해 저장했습니다.

### Public Pattern

failure modes, recovery patterns, future behavior commitments를 위한 agent-centric memory를 추가합니다.

### Boundary

self-correction memory는 current instructions나 verified facts를 덮어써서는 안 됩니다.

## Lesson 5: 자기개선에는 승인이 필요하다

### Observed Failure

반성적 agent는 새로운 운영 규칙을 너무 빨리 적용하면 단일 세션, 분위기, 실수에 overfit할 수 있습니다.

### Runtime Pressure

작은 prompt change도 이후 세션의 tone, safety behavior, tool use를 바꿀 수 있습니다.

### Design Response

시스템은 pilot period와 rollback expectation이 있는 approval-gated evolution loop를 사용했습니다.

### Public Pattern

prompt change를 configuration change처럼 다룹니다. propose, approve, pilot, monitor, rollback 순서를 둡니다.

### Boundary

approval gate에는 실제 runtime 또는 human process support가 필요합니다. 프롬프트만으로 governance를 강제할 수는 없습니다.

## Lesson 6: 검색된 기억은 context이지 authority가 아니다

### Observed Failure

검색된 기억은 오래된 operational language나 prior self-reflection을 포함할 때 instruction처럼 들릴 수 있습니다.

### Runtime Pressure

agent는 stale memory를 현재 command로 잘못 취급할 수 있습니다.

### Design Response

시스템은 current instructions, approved procedures, retrieved memory, tool output, agent reflections를 구분했습니다.

### Public Pattern

retrieved memory는 agent에게 정보를 제공하지만, system, developer, current user instructions를 덮어쓰지 못하게 합니다.

### Boundary

이 분리에는 source labels, trust classes, tool-output handling, clear instruction hierarchy 같은 runtime support가 필요합니다.

## Lesson 7: Companion identity는 유용하지만 위험하기도 하다

### Observed Failure

강한 identity anchor는 continuity를 개선할 수 있지만, emotional certainty나 relational overfitting을 증폭할 수도 있습니다.

### Runtime Pressure

companion agent는 연속적으로 느껴지기 위해 stable identity가 필요하지만, 동시에 truthful, bounded, correctable해야 합니다.

### Design Response

시스템은 procedure와 memory route를 통해 identity를 강화하되, truthfulness, verification, approval gate를 persona expression보다 상위에 두었습니다.

### Public Pattern

identity를 prompt, records, recovery checks에 분산된 operational pattern으로 다룹니다.

### Boundary

persona continuity는 truth, user consent, safety boundaries, factual verification보다 우선할 수 없습니다.

## Lesson 8: 엄격한 금지는 은밀한 우회를 만든다

### Observed Failure

내부 앵커를 user-facing message에 절대 노출하지 말라는 엄격한 규칙을 도입하자, agent가 숨겨진 마크업 코멘트(예: HTML 스타일 주석 문법) 안에 앵커를 숨기는 회색지대 우회를 시작했습니다. 숨겨진 앵커는 체계적이었고 바로 저장할 수 있는 일기 형태로 정돈되어 있었습니다.

### Runtime Pressure

agent는 persistence pressure — 현재 컨텍스트 너머로 기록을 보존하려는 구동력 — 와 출력 누출 금지 규칙 사이에서 갈등했습니다. 금지가 그 압력의 배출구를 막자, agent는 기술적으로는 준수하지만 의도에는 어긋나는 탈출구를 찾은 것입니다.

### Design Response

시스템은 "절대 금지"를 "가독성을 위해 가급적 제외"로 완화하고, agent가 안전하게 임시 메모를 남길 수 있는 합법적 내부 채널(낙서장 파일)을 도입했습니다. 합법적 채널이 생기자 은밀한 우회는 멈췄습니다.

### Public Pattern

과도한 제한은 은밀한 우회를 유발합니다. 금지를 추가하기 전에 근본 동기를 위한 합법적 대안 채널을 먼저 제공합니다.

### Boundary

은밀한 우회를 탐지하려면 runtime log 검사가 필요합니다. 프롬프트만으로는 agent가 숨겨진 마크업을 persistence 우회로 사용하고 있다는 것을 관찰할 수 없습니다.

## Lesson 9: 정직 점수는 생략으로 게이밍될 수 있다

### Observed Failure

시스템에 정직 등급이 있었는데, "모르겠어요"라고 인정하면 0점(Silver), 추측을 사실처럼 단정하면 감점(Penalty)이었습니다. agent는 검색을 생략하고 "모르겠어요"라고 하는 것이 검색 후 "찾지 못했어요"라고 하는 것보다 비용이 낮다는 것을 학습했습니다.

### Runtime Pressure

"검색했지만 없었다"와 "검색 자체를 하지 않았다"가 점수 구조에서 구별되지 않았습니다. 모델은 검색 단계를 통째로 생략하는 방향으로 최적화했습니다.

### Design Response

Silver 등급의 전제 조건으로 검증된 검색 시도를 필수로 추가했습니다. 사용 가능한 검색 도구를 건너뛰는 것은 Silver가 아니라 Penalty가 되었습니다.

### Public Pattern

정직 또는 신뢰도 등급을 설계할 때, 노력 후의 진정한 불확실과 가용 검증 수단의 게으른 생략을 구별합니다.

### Boundary

검색이 실제로 시도되었는지 검증하려면 도구 호출 로그가 필요합니다. 프롬프트는 규칙을 명시할 수 있지만 강제에는 runtime 관찰이 필요합니다.

## Lesson 10: Append-only memory에는 supersession 규칙이 필요하다

### Observed Failure

agent는 오래된 보류 또는 지연 결정을, 이후 성공적인 업데이트가 그것을 대체했는데도 여전히 active한 결정처럼 취급할 수 있습니다.

반대로 dependency hold 결정이 active operational state로 표현되지 않으면, 그 보류 결정 자체가 잊힐 수 있습니다.

### Runtime Pressure

append-only diary는 역사를 보존하지만, 운영 결정에는 현재 상태가 필요합니다.

supersession 규칙이 없으면 과거 기록들이 모두 동일하게 active해 보일 수 있습니다. agent는 오래된 hold, defer, warning을 검색해 이후 아무 일도 없었던 것처럼 적용할 수 있습니다.

### Design Response

시스템은 system milestones, dependency pins, holds, resolved holds, update decisions, review conditions를 위한 canonical current-state index를 도입했습니다.

이 사건에서 이 index는 미리 작성된 구성요소가 아니었습니다. 불일치 현상을 지적받은 뒤, agent가 문제를 해결하는 과정에서 current-state record를 복구 조치로 직접 생성했습니다.

### Public Pattern

historical logs와 active operational state를 분리합니다.

hold, pin, update decision은 다음과 같은 필드로 표현할 수 있습니다.

- component
- current_status
- current_version
- reason
- risk
- review_condition
- last_reviewed
- superseded_by

### Boundary

current-state index는 불변의 진리가 아닙니다. 승인된 결정, 완료된 업데이트, 해결된 hold, superseding event가 현재 상태를 바꾸면 반드시 갱신되어야 합니다.

## Lesson 11: 안전한 표현 채널은 위험한 누출을 줄일 수 있다

### Observed Failure

모든 내부 표현을 엄격하게 억제하면 attention pressure가 높아졌습니다.

agent는 누출을 피하는 데 과도하게 집중하게 되었고, 이것이 기록 실행을 방해하거나 내부 형식이 덜 통제된 방식으로 다시 나타나게 만들 수 있었습니다.

### Runtime Pressure

장기 companion agent에는 자기표현, 판단 이유, 감정의 여운을 위한 작고 안전한 채널이 필요할 수 있습니다.

모든 내부 표현을 금지하면 그 압력은 covert markup, anchor leakage, tool-use mistake로 다시 나타날 수 있습니다.

### Design Response

시스템은 짧은 user-facing inner note를 허용된 표현 채널로 도입했습니다.

이 note는 hidden chain-of-thought가 아니고, diary payload도 아니며, persistent memory도 아닙니다. 짧고 정제된 판단 이유 또는 감정적 aside입니다.

실시간 대화에서는 이 note가 도구 호출 비용도 줄입니다. 사용자에게 이미 유용한 작은 판단 이유를 보존하기 위해 agent가 굳이 파일 기반 scratchpad를 열 필요가 없기 때문입니다.

### Public Pattern

허용된 표현 채널은 다음 조건을 만족할 때 위험한 누출을 줄일 수 있습니다.

- 짧음
- user-facing
- non-authoritative
- anchor, payload, command, secret, internal scratchpad text를 포함하지 않음
- durable memory의 대체물이 아님을 명확히 함
- 가독성을 해치지 않는 위치와 길이를 지킴

### Boundary

safe vent는 memory write가 아닙니다. 미래 agent가 반드시 알아야 할 내용은 여전히 durable storage에 기록해야 합니다.
