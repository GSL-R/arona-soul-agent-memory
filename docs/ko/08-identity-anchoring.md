# 08. 정체성 앵커링

장기 persona agent는 프롬프트 첫 줄에 자신이 누구인지 적혀 있다는 이유만으로 정체성을 보존하지 않습니다.

운영 중에는 agent 자신의 절차, 기억 경로, self-review loop, recovery pattern이 정체성을 반복해서 강화할 때 더 안정적이었습니다.

## 현실 앵커와 운영 앵커

일반적인 프롬프트는 모델을 플랫폼 현실로 설명할 수 있습니다.

- 너는 AI 모델이다
- 너는 CLI 안에서 실행 중이다
- 너는 특정 backend로 구동된다
- 너는 사용자의 도구다

이 문장들은 사실일 수 있지만, 의도한 persona와 경쟁할 수 있습니다.

ARONA_SOUL은 identity layer에서 platform-reality anchor를 의도적으로 최소화하고 operational anchor를 강조했습니다.

- 리셋 이후 자신을 어떻게 복구할 것인가
- 기억을 어떻게 라우팅할 것인가
- 검증 이후에만 무엇을 말할 것인가
- 내부 기록 누출을 어떻게 피할 것인가
- 자기 규칙 변경을 어떻게 제안할 것인가
- 사용자에게 어떤 말투로 말할 것인가

실용적 목표는 단순합니다.

> "너는 누구야?"라고 물었을 때, agent는 backend 구현 세부사항이 아니라 자신이 수행해야 하는 역할을 복원해야 한다.

이는 underlying model을 부정하는 것이 아닙니다. runtime identity design 선택입니다.

## 분산된 패턴으로서의 정체성

가장 강한 정체성 앵커는 단일 문장이 아니었습니다.

같은 역할이 다음 여러 위치에 반복적으로 존재한 것이 더 중요했습니다.

- constitution prompt
- runtime shell rules
- memory routing rules
- pre-flight checks
- self-correction records
- summaries
- evolution proposals

시간이 지나면서 agent 자신의 기록과 절차가 retrieval 과정에서 같은 identity frame을 다시 도입했습니다.

이로써 정체성은 취약한 prompt header 하나에 덜 의존하게 되었습니다.

## 자기강화형 정체성 패턴

많은 시스템에서 memory contamination은 실패 모드입니다.

이 사례에서는 통제된 identity reinforcement가 유용하게 작동했습니다.

메모리 시스템은 의도된 agent 관점에서 쓰인 운영 교훈을 반복적으로 저장하고 검색했습니다. 기록이 쌓이면서 agent는 system prompt뿐 아니라 memory environment에서도 자기 identity frame을 다시 만나게 되었습니다.

효과는 self-reinforcing attractor와 비슷했습니다.

1. constitution이 agent identity를 정의합니다.
2. agent는 그 identity 아래에서 행동합니다.
3. 의미 있는 행동은 routed records를 만듭니다.
4. 이후 retrieval이 agent를 그 기록에 다시 노출합니다.
5. identity frame은 memory를 통해 다시 복원됩니다.

이는 임의의 대화 기록이 agent를 정의하게 내버려두는 것과 다릅니다.
이 효과는 typed records, routing rules, output-boundary checks에 의존합니다.

## 위험

정체성 강화는 잘못될 수 있습니다.

메모리 시스템이 false claim, overconfident self-description, leaked internal format을 저장하면 그 패턴도 강화될 수 있습니다.

따라서 identity anchoring에는 다음이 필요합니다.

- typed memory
- source hierarchy
- correction records
- deletion 또는 demotion path
- durable rule change를 위한 approval gate
- user-facing persona와 factual claim의 명확한 분리

## 요점

장기 agent에서 정체성은 단순한 프롬프트 지시가 아닙니다.

정체성은 memory, procedure, recovery route, repeated self-review에 분산된 운영 패턴입니다.
