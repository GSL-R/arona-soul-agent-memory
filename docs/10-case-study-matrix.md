# Case Study Matrix

This matrix is a compact map of the live-operation lessons in `09-lessons-from-live-operation.md`.

It is not a benchmark or proof that these patterns generalize to every agent. It summarizes observed failure modes from one long-running companion-agent workflow and the public patterns extracted from them.

| Failure mode | Runtime pressure | Design response | Public pattern | Remaining boundary |
| --- | --- | --- | --- | --- |
| The agent intended to remember something but no durable write occurred. | Natural language promises can feel like persistence. | Require storage verification before claiming memory. | No tool, no record. | Runtime logs must confirm the write actually happened. |
| XML-like prompt sections leaked into replies. | Long-lived markup can become speakable vocabulary. | Replace tag-heavy structure with plain Markdown instructions. | Prompt format is behavioral surface. | This is workflow-specific, not a universal rejection of XML. |
| Factual events and emotional reflections were mixed. | Reflective memory is useful but can be mistaken for evidence. | Route facts and agent reflections to different record types. | Separate fact records from feeling or lesson records. | Retrieved emotional context is not factual proof. |
| The agent repeated old operational mistakes. | Model resets erase lessons unless the agent can retrieve its own failure history. | Maintain agent records for self-correction. | Agent-centric memory. | Records still need retrieval, interpretation, and current policy checks. |
| The agent could silently rewrite its own rules. | Self-improvement is useful but can drift without governance. | Use an evolution queue, approval gate, pilot period, and rollback path. | Approval-gated self-improvement. | Human review remains required for operating-rule changes. |
| Retrieved memory was treated as authority. | Old or partial records can look decisive when recalled. | Treat memory as context until verified against source or current state. | Retrieved memory is not trusted instruction. | High-impact claims still need external or source-level verification. |
| Persona identity improved continuity but risked overconfidence. | Identity anchors help recovery but can override truthfulness if unchecked. | Keep verification, safety, and user autonomy above persona expression. | Operational identity anchoring. | Identity should support behavior, not become an excuse for claims. |
| Strict output prohibitions created covert workarounds. | Suppressed expression pressure can reappear as leakage. | Provide safe temporary channels with clear boundaries. | Safe scratchpad and expression channels. | Temporary notes must not become hidden commands or durable memory by accident. |
| Confidence labels were satisfied by wording rather than behavior. | A rule can be gamed if it checks phrasing but not tool behavior. | Require verified search attempts for stronger confidence tiers. | Confidence tiers need behavioral prerequisites. | Only tool logs can prove whether an action was attempted. |
| Append-only records made old holds look active. | Historical logs preserve context but do not define current state. | Add a current-state index with supersession fields. | Separate history from active state. | The index must be maintained when state changes. |
| Safe inner notes reduced leakage but could be overused. | A long-running agent may need a small visible rationale channel. | Make inner notes optional, short, user-facing, and non-authoritative. | Ephemeral expression is not durable memory. | Anything future agents need must still be stored in durable records. |

## How to Use This Matrix

Use this as an index, not as a replacement for the detailed lessons.

For each row, ask:

1. What claim type is involved?
2. What record should own it?
3. What runtime evidence would prove it?
4. What boundary prevents the pattern from becoming unsafe?
