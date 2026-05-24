# Example: Dual Record Routing

This is a fictional example of routing a single event into two separate memory records.

## Scenario

The user reports that a long-running automation script crashed overnight. The agent investigates, identifies the root cause, fixes the configuration, and verifies the fix.

## Live Record (Factual)

```md
### 2026-05-20 09:15 — Automation Recovery

- heartbeat scheduler stopped responding after 03:00
- root cause: stale lock file from interrupted previous run
- fix: removed lock file, added cleanup step to startup sequence
- verified: scheduler ran successfully at 09:20
- status: [DONE]
```

## Agent Record (Reflective)

```md
### 2026-05-20 09:30 — Lesson from overnight failure

This was the second time a stale lock file caused a silent failure.
Last time I only fixed the symptom. This time I added a cleanup step
so future sessions inherit a safer startup sequence.

I need to remember: when something fails silently, the fix should
make the failure visible next time, not just recover from it.
```

## Why Two Records?

The live record answers: **what happened and what changed?**
The agent record answers: **what did the agent learn and what should it avoid next time?**

If these were merged into one record:

- the factual log would be contaminated with self-reflection
- retrieval for "what changed in the scheduler?" would return emotional language
- retrieval for "what has the agent learned about silent failures?" would return implementation details

Separate routing preserves each record's purpose during future recall.

## Lesson

Some events need both a factual record and a reflective record. The routing system should support dual writes without merging them.
