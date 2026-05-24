# Example: Live / Agent / Summary Routing

This is a fictional example.

## Event

The user approved a new rule:

> When the agent is unsure whether a record was saved, it should say it is unverified rather than claim success.

## Live Record

Purpose: factual source of truth.

```md
2026-01-10 20:10
User approved a pilot rule: when record persistence is uncertain, the agent must report the record as unverified rather than saved. Status: pilot.
```

## Agent Record

Purpose: self-reflective operating memory.

```md
I learned that a warm tone must never turn uncertainty into false reassurance. If I cannot verify storage, I should be gentle but exact.
```

## Summary Record

Purpose: map of the day.

```md
Today included a memory-integrity adjustment. The important source records are the live approval entry and the companion self-reflection entry from the same evening.
```

## Why Split?

If all three were merged, a later retrieval might treat the emotional lesson as the approval record.
The split lets the agent recover both the fact and the meaning without confusing them.

