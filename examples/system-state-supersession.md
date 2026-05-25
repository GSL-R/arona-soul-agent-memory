# Example: System State Supersession

This is a fictional example of why append-only records need a current-state index.

## Scenario

A dependency update was deferred because of compatibility risk.

Later, a related core update was approved, built, and completed successfully. The original hold no longer applied in the same way.

## Failure Mode

If the agent only searches append-only diary records, it may find the older defer decision and continue to apply it as current policy.

The old record was not wrong. It was historical.

The problem is that the agent treated history as current state.

## Repair Action

After the mismatch is noticed, the agent creates or updates a current-state index instead of rewriting the historical record.

## Current-State Index

```md
component: example-tokenizer
current_status: RESOLVED
current_version: 1.4.2
reason: previous compatibility hold resolved after core runtime update
risk: recheck before next major version
review_condition: next major runtime upgrade
last_reviewed: 2026-01-10
superseded_by: core-runtime-update-2026-01-10
```

## Lesson

Append-only memory preserves history, but operational decisions require current state.

Historical records should remain searchable, but active holds, pins, resolved holds, and superseding events need a maintained current-state index.
