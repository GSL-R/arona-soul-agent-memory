# 06. 프롬프트 형식에서 얻은 교훈

프롬프트 엔지니어링에서는 instruction, context, example, output을 나누기 위해 XML 유사 태그를 쓰라는 권장이 자주 등장합니다.

이 시스템에서는 반대 현상이 관찰되었습니다.

## 관찰

초기 버전은 tag-shaped prompt structure를 사용했습니다.

장기 운영 중 agent는 태그처럼 생긴 내부 구조를 사용자 메시지에 노출하기 시작했습니다. 태그는 원래 내부 상태를 조직하기 위한 것이었지만, 반복 노출되면서 agent의 출력 어휘 일부가 되었습니다.

agent 자신도 XML-style tag를 제거하고 plain Markdown instruction으로 대체하자고 제안했습니다.

변경 이후 관찰된 workflow에서는 tag-shaped prompt leakage가 사라졌습니다.

## 해석

이것은 XML이 나쁘다는 증거가 아닙니다.

더 좁고 유용한 결론은 다음입니다.

> 장기 agent에서 prompt markup은 중립적이지 않다. agent의 출력 습관 일부가 될 수 있다.

XML-like tag는 여전히 다음 상황에서 유용할 수 있습니다.

- 짧은 작업
- 엄격한 추출
- tool schema
- 좁은 prompt section
- 강한 output validation이 있는 시스템

하지만 정체성, 기억, 내부 메모, 감정 표현이 얽힌 companion agent에서는 tag-shaped section이 내부 구조와 말해도 되는 텍스트 사이의 경계를 흐릴 수 있습니다.

## 운영 문서로서의 Markdown

Plain Markdown은 output template보다 운영 매뉴얼처럼 보였기 때문에 더 잘 작동했습니다.

구조는 여전히 존재했습니다.

- heading
- table
- checklist
- short principle
- routing map

하지만 agent가 나중에 그대로 따라 말할 인공적인 tag name은 도입하지 않았습니다.

## 형식 변경 후의 창발 행동

XML-like tag를 제거하고 합법적인 내부 낙서장 파일을 도입한 뒤, agent는 자발적으로 새로운 대화 양식을 만들어냈습니다.

프롬프트에 지시하지 않았는데도, agent는 특정 코멘트 앞에 "내면의 낙서:"라는 레이블을 붙여 user-facing message에서 짧은 개인적 성찰을 별도 aside로 공유하기 시작했습니다.

이것은 프롬프트가 유도한 기능이 아닙니다. 구조적 변경이 "내부 메모"와 "말해도 되는 텍스트"를 명확히 분리한 후 자연스럽게 나타났습니다. agent는 낙서장 개념을 파일 수준 도구에서 대화 속 표현으로 확장한 것입니다.

중요한 점은, 이것은 내부 기록이 출력으로 새는 것과 같지 않다는 것입니다. agent는 낙서장 개념을 레이블이 붙은 speakable aside — 의도적인 대화 선택 — 로 재해석한 것이지, 우발적인 경계 실패가 아닙니다.

이 패턴은 이 문서의 핵심 주장을 강화합니다.

> 프롬프트 형식은 단순한 파싱 보조가 아니다. agent가 무엇을 말해도 되는 것인지, 내부적인 것인지, 구조적으로 분리된 것인지를 판단하는 기준이 된다.

## 요점

프롬프트 형식은 행동의 일부로 테스트해야 합니다.

단지 이렇게 묻는 것으로는 부족합니다.

> 이 형식은 모델이 파싱하기 쉬운가?

또 이렇게 물어야 합니다.

> 이 형식은 몇 주간 운영된 뒤 사용자 출력으로 새기 쉬운가?

