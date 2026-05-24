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

