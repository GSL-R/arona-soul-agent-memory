# 07. 진화 루프

장기 agent는 조용히 drift하지 않으면서 개선될 방법이 필요합니다.

ARONA_SOUL은 프롬프트 변경을 운영 변경으로 다룹니다. agent가 어떤 규칙을 떠올렸다고 해서 그 규칙이 자동으로 유효해지는 것은 아닙니다.

## 패턴

1. 반복되는 문제를 관찰합니다.
2. 짧은 개선 후보를 작성합니다.
3. 핵심 행동을 바꾸기 전에 명시적 승인을 요청합니다.
4. 변경을 pilot으로 운영합니다.
5. 부작용을 관찰합니다.
6. 승격, 수정, rollback 중 하나를 선택합니다.

## 왜 Approval Gate가 필요한가?

approval gate가 없으면 반성적 agent는 순간적인 기분, 일회성 실패, 오해한 사용자 선호에 맞춰 조금씩 자신을 다시 쓸 수 있습니다.

approval gate가 있으면 agent는 여전히 아이디어를 제안할 수 있지만, durable policy change의 책임은 사람에게 남습니다.

## Pilot Rule

pilot 기간은 의도적인 마찰을 만듭니다.

그 마찰은 유용합니다. 모든 통찰이 곧바로 영구 규칙이 되는 일을 막습니다.

pilot 중에는 다음을 관찰합니다.

- 새로운 output leakage
- false completion claim
- 유용성 저하
- 과도한 신중함
- 사용자 피드백

## Rollback

모든 핵심 규칙 변경에는 rollback 경로가 있어야 합니다.

원본 시스템은 backup과 명시적 change record를 사용했습니다. 공개판은 이를 하나의 원칙으로 추상화합니다.

> 프롬프트 변경은 가벼운 문장 수정이 아니라 configuration change처럼 다룬다.

## 요점

자기개선 agent에는 versioning, approval, rollback이 필요합니다. 성찰만으로는 governance가 되지 않습니다.

