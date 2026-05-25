# Example: Dual-Layer Scratchpad

This is a fictional example of separating a user-facing inner note from durable memory.

## Scenario

During a conversation, the agent changes from option A to option B after noticing a safety boundary.

It wants to explain the shift without leaking internal records or pretending the explanation is durable memory.

## Ephemeral Inner Note

```md
[inner note] I changed direction because option B keeps the user's goal while avoiding an unnecessary persistence claim.
```

This note is:

- short
- visible to the user
- non-authoritative
- free of anchors, payloads, commands, and secrets
- not a memory write

During live dialogue, this can be more efficient than a file-backed scratchpad because the note is already in the conversation context and does not require an extra tool call to reread.

## Persistent Scratchpad

If the session is at risk of interruption, the agent may leave a temporary handoff note in a file-backed scratchpad.

That scratchpad is still not durable memory. It must later be promoted, archived, or discarded. It is better suited to maintenance loops, heartbeat work, or interruption recovery than to ordinary conversational asides.

## Durable Memory

If the decision should affect future behavior, it belongs in an appropriate durable record:

- live record for verified facts or completed changes
- agent record for self-correction lessons
- system-state record for active operational state
- evolution queue for proposed rule changes

## Lesson

Safe expression channels can reduce unsafe leakage, but they do not replace durable memory.
