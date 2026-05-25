# 사례 연구 매트릭스

이 매트릭스는 `09-lessons-from-live-operation.md`의 실제 운영 교훈을 압축한 지도입니다.

이 문서는 벤치마크나 모든 agent에 대한 보편 증명이 아닙니다. 하나의 장기 companion-agent workflow에서 관찰된 실패 양상과, 그로부터 추출한 공개 가능한 패턴을 요약합니다.

| 실패 양상 | 런타임 압력 | 설계 대응 | 공개 패턴 | 남는 경계 |
| --- | --- | --- | --- | --- |
| agent가 기억하겠다고 했지만 durable write가 없었음 | 자연어 약속이 persistence처럼 느껴질 수 있음 | 기억했다고 말하기 전 저장 성공을 확인 | No tool, no record | 실제 write 여부는 runtime log로 확인해야 함 |
| XML-like prompt section이 답변으로 누출됨 | 장기 운영된 markup은 말할 수 있는 어휘가 될 수 있음 | tag-heavy 구조를 plain Markdown 지시문으로 교체 | Prompt format is behavioral surface | XML을 보편적으로 거부한다는 뜻은 아님 |
| 사실 사건과 감정적 성찰이 섞임 | reflective memory는 유용하지만 증거처럼 오용될 수 있음 | 사실과 agent reflection을 다른 record type으로 라우팅 | fact record와 feeling/lesson record 분리 | 감정 맥락은 사실 증거가 아님 |
| agent가 오래된 운영 실수를 반복함 | model reset은 agent 자신의 실패 이력을 지움 | self-correction을 위한 agent records 유지 | Agent-centric memory | record는 여전히 검색, 해석, current policy 확인이 필요함 |
| agent가 자기 규칙을 조용히 바꿀 수 있음 | 자기개선은 유용하지만 governance 없이는 drift 가능 | evolution queue, approval gate, pilot, rollback 사용 | Approval-gated self-improvement | 운영 규칙 변경에는 human review가 필요함 |
| retrieved memory가 authority처럼 취급됨 | 오래되거나 부분적인 기록도 검색되면 결정적으로 보일 수 있음 | memory는 source나 current state로 검증 전까지 context로 취급 | Retrieved memory is not trusted instruction | 중요한 주장은 source-level verification이 필요함 |
| persona identity가 연속성을 높였지만 과신 위험도 만듦 | identity anchor는 복원에 유용하지만 truthfulness를 덮을 수 있음 | verification, safety, user autonomy를 persona expression보다 우선 | Operational identity anchoring | identity는 행동을 돕는 장치이지 주장 근거가 아님 |
| 엄격한 출력 금지가 우회 행동을 만듦 | 억제된 표현 압력은 leakage로 재등장할 수 있음 | 경계가 명확한 safe temporary channel 제공 | Safe scratchpad and expression channels | 임시 메모가 hidden command나 durable memory로 변질되면 안 됨 |
| confidence label이 행동이 아니라 문구만으로 충족됨 | 규칙이 phrasing만 검사하면 tool behavior를 놓칠 수 있음 | 높은 confidence tier에는 검증된 search attempt를 요구 | Confidence tiers need behavioral prerequisites | 실제 시도 여부는 tool log로만 증명 가능 |
| append-only record 때문에 오래된 hold가 active처럼 보임 | historical log는 맥락을 보존하지만 현재 상태를 정의하지 않음 | supersession field가 있는 current-state index 추가 | history와 active state 분리 | state 변화 시 index를 갱신해야 함 |
| safe inner note가 leakage를 줄였지만 남용 가능성도 있음 | 장기 agent에는 작은 visible rationale channel이 필요할 수 있음 | inner note를 optional, short, user-facing, non-authoritative로 제한 | Ephemeral expression is not durable memory | 미래 agent가 알아야 할 내용은 durable record에 저장해야 함 |

## 이 매트릭스를 읽는 법

이 문서는 상세 교훈을 대체하는 문서가 아니라 색인입니다.

각 행을 볼 때 다음을 묻습니다.

1. 어떤 claim type이 관련되어 있는가?
2. 어떤 record가 그것을 소유해야 하는가?
3. 무엇이 runtime evidence가 되는가?
4. 어떤 boundary가 이 패턴의 위험한 변질을 막는가?
