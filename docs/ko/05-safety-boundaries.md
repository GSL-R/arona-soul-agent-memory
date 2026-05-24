# 05. 안전 경계

장기 agent는 종종 내부 자료를 생성합니다.

- memory payload
- anchor
- tool command
- scratch note
- status label
- recovery instruction

이 구조들이 사용자 메시지로 새면 두 가지 일이 발생합니다.

첫째, 사용자는 내부 구현 노이즈를 보게 됩니다.
둘째, 모델은 그 문자열을 정상적인 대화 출력으로 학습하고 이후 반복할 수 있습니다.

## 경계 규칙

공개판 ARONA_SOUL 패턴은 단순한 규칙을 사용합니다.

> 내부 기록은 도구나 durable storage에 속하고, 사용자 메시지는 사용자에게 속한다.

이 규칙은 다음 운영 규칙으로 이어집니다.

- 저장 대신 memory payload를 출력하지 않음
- storage tool이 성공하기 전에는 저장되었다고 말하지 않음
- 일반 답변에 내부 anchor나 command-shaped text를 노출하지 않음
- 기록 실패 시 payload를 덤프하지 않고 실패 사실만 보고함

## No Tool, No Record

"No tool, no record"는 핵심 문장입니다.

agent는 무엇인가를 기억하려는 의도를 가질 수 있지만, 의도는 persistence가 아닙니다. write operation이 실제로 일어나지 않았다면, agent는 그 사건을 기억하거나 저장했다고 말하면 안 됩니다.

이는 false memory가 missing memory보다 더 위험하기 때문입니다. 미래의 agent가 존재하지 않는 기록을 전제로 행동할 수 있습니다.

## Pre-Flight Check

최종 출력 전에 agent는 다음을 확인합니다.

- 지금 말하려는 주장을 실제로 검증했는가?
- 내부 기록 텍스트가 사용자 메시지에 섞이지 않았는가?
- 내부 명령, anchor, payload를 노출하지 않았는가?
- 추측을 사실처럼 다루지 않았는가?
- 승인 없이 규칙을 바꾸지 않았는가?

이는 행동 체크리스트이지 그 자체로 보안 경계는 아닙니다. 주변 runtime은 여전히 sanitize, validate, tool 제한을 수행해야 합니다.

## 요점

프롬프트 규칙은 runtime safety를 대체할 수 없습니다. 하지만 tool 제약과 결합될 때 반복적인 행동 실패를 줄일 수 있습니다.

