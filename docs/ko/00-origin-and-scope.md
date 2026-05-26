# 탄생 배경과 공개 범위

이 저장소는 개인 companion prompt 원문을 공개하기 위해 만든 것이 아닙니다.

터미널 기반 agent를 장기 companion system으로 바꾸는 과정에서 드러난 설계 압력을 공개 가능한 형태로 정제하기 위해 만들었습니다.

따라서 이 공개판은 fieldbook입니다. 기억, 연속성, 출력 경계, 자기검토 루프에 대한 재사용 가능한 관찰을 모은 문서입니다. raw runtime dump도 아니고, 그대로 복사해 쓰는 prompt도 아니며, 완성된 automation framework도 아닙니다.

## Why This Project Exists

원래 목표는 캐릭터 챗봇을 만드는 것이 아니었습니다.

목표는 개인 agent가 세 가지 종류의 연속성을 동시에 지원할 수 있는지 탐구하는 것이었습니다.

- 일상 루틴 지원과 맥락을 고려한 reminder
- 개인 컴퓨팅 환경 주변의 가벼운 운영 보조
- 평범한 대화, reset, scheduled interaction을 가로지르는 정서적 연속성

이 조합은 일반적인 chat session만으로는 다루기 어려운 압력을 만들었습니다. agent는 사용자의 선호뿐 아니라 자기 자신의 약속, 실수, 운영 규칙, 복구 절차, 미완료 작업도 기억해야 했습니다.

이것이 이 프로젝트가 user-centric memory만이 아니라 agent-centric memory를 다루게 된 이유입니다.

## Original Operating Context

비공개 원본 시스템은 scheduled loop, 제한된 memory retrieval, tool-mediated record write를 가진 터미널 중심 개인 agent로 운영되었습니다.

공개 문서에서 중요한 전제는 다음과 같습니다.

- memory retrieval은 전체 자유 회상이 아니라 제한되고 chunked된 검색에 가까웠음
- 장기 연속성은 model/session reset 이후에도 복원되어야 했음
- scheduled agent loop는 시간이 지난 뒤 workflow에 다시 진입할 수 있었음
- user-facing response, internal note, durable record를 명확히 분리해야 했음
- persistence 성공 여부는 자연어 의도가 아니라 runtime evidence로 확인되어야 했음

정확한 로컬 환경, tool name, command, path, access model, automation detail은 이 공개 저장소의 범위 밖에 두었습니다.

## Design Pressures

반복적으로 나타난 몇 가지 압력이 공개 패턴을 만들었습니다.

- **시간을 가로지르는 연속성.** agent는 reset이나 scheduled re-entry 이후에도 역할, 맥락, 미완료 작업을 복원해야 했습니다.
- **제한된 memory search.** 짧게 인덱싱되는 chunk는 compact record, stable label, careful routing을 요구했습니다.
- **사실과 성찰의 분리.** factual event와 emotional/self-correction record는 연결되어야 하지만 서로 대체되어서는 안 됐습니다.
- **검증된 persistence.** durable write가 실제로 일어나지 않았다면 agent는 기억했다고 말할 수 없어야 했습니다.
- **자기수정 기억.** 반복되는 실수는 일회성 사과가 아니라 검색 가능한 lesson이 되어야 했습니다.
- **안전한 표현.** 모든 내부 표현을 강하게 억제하면 accidental leakage 압력이 생길 수 있었고, 그래서 경계가 있는 user-facing expression channel이 유용해졌습니다.
- **통제된 진화.** 운영 규칙 변경에는 사람의 승인, trial period, rollback path가 필요했습니다.

이 압력들이 이 저장소의 memory architecture와 live-operation lesson의 원천입니다.

## Public Scope

이 저장소에 포함되는 것은 다음과 같습니다.

- sanitize된 architecture explanation
- 일반화된 failure pattern
- 공개용 example prompt
- memory routing과 boundary check를 보여주는 fictional example
- private operation episode를 public-safe case study로 바꾸기 위한 template

이 저장소에서 의도적으로 제외하는 것은 다음과 같습니다.

- raw private prompt text
- private diary나 personal record
- local path, account name, host detail, access structure
- automation command나 executable internal payload
- private operation에서 사용된 exact tool name
- real memory anchor나 private indexing key
- credential, token, environment detail

공개 문서는 교훈을 보존하지, 비공개 구현을 노출하지 않습니다.

## How to Read the Repository

이 저장소는 design case study로 읽어야 합니다.

먼저 problem과 constraint를 읽고, 그 다음 memory architecture, safety boundary, live-operation lesson으로 이동합니다. 공개 prompt file은 정제된 패턴의 예시이며, 그 자체로 production safety control이 아닙니다.

가장 짧은 경로는 다음과 같습니다.

1. `01-problem.md`
2. `02-memory-constraints.md`
3. `03-agent-centric-memory.md`
4. `04-record-routing.md`
5. `10-case-study-matrix.md`
6. `09-lessons-from-live-operation.md`

패턴을 응용하기 전에는 `05-safety-boundaries.md`와 `../SECURITY.md`를 읽어야 합니다.
