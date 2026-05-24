# 07. Evolution Loop

Long-running agents need a way to improve without silently drifting.

ARONA_SOUL treats prompt changes as operational changes. A new rule is not automatically valid just because the agent thought of it.

## Pattern

1. Observe a repeated issue.
2. Write a short improvement candidate.
3. Ask for explicit approval before changing core behavior.
4. Run the change as a pilot.
5. Watch for side effects.
6. Promote, revise, or roll back.

## Why an Approval Gate?

Without an approval gate, a reflective agent can gradually rewrite itself around transient moods, one-off failures, or misunderstood user preferences.

With an approval gate, the agent can still contribute ideas while the human remains responsible for durable policy changes.

## Pilot Rule

A pilot period creates friction.

That friction is useful. It prevents every insight from becoming permanent law.

During a pilot, the system watches for:

- new output leakage
- false completion claims
- degraded usefulness
- over-cautious behavior
- user feedback

## Rollback

Every core rule change should have a rollback path.

The original system used backups and explicit change records. The public version abstracts that into one principle:

> Treat prompt changes like configuration changes, not casual prose edits.

## Takeaway

Self-improving agents need versioning, approval, and rollback. Reflection alone is not governance.

