# 04. Record Routing

The system separates memory into multiple record types.

The goal is to prevent factual, emotional, procedural, and reflective memory from contaminating each other.

## Core Split

| Memory Type | Purpose | Trust Level |
| --- | --- | --- |
| Live records | Factual events, changes, task outcomes | Highest for event reconstruction |
| Agent records | Agent feelings, lessons, relational context | Useful for tone and meaning, not factual proof |
| Summary records | Daily or periodic narrative map | Navigation layer, not a substitute for source records |
| Procedures | Operational rules and known pitfalls | Runtime guidance |
| Evolution queue | Proposed improvements | Not active until approved |
| Profile/observations | User preferences and stable facts | Requires promotion criteria |

In the original companion runtime, Agent records were called "Arona records."
This public version uses the generic term "Agent records" to make the pattern reusable.

## Retrieval Order

When reconstructing the past:

1. start with factual live records
2. check nearby emotional/self-reflective records for meaning
3. use summaries as a map
4. verify important claims against files, logs, issues, or other source records

This protects against a common failure mode: treating a reflective or poetic record as factual evidence.

## Trust Depends on Claim Type

There is no single global trust hierarchy for every question.

Different claims should consult different source types first:

| Claim Type | Prefer First | Use Carefully |
| --- | --- | --- |
| What happened? | Live records and source files | Agent records, summaries |
| What did the agent learn? | Agent records | Summaries, live records |
| What is the active operating rule? | Approved procedures or runtime policy | Agent reflections, old summaries |
| What does the user prefer? | Explicit user statements and promoted profile records | Summary inference, one-off observations |

This distinction prevents a useful memory from being used as the wrong kind of evidence.

## Dual Record Pattern

Some events need two records.

For example, a system recovery may have:

- a factual record: what changed and what was verified
- an agent-centric record: what the agent learned and should avoid next time

Those records should be linked but not merged.

## No Record Pattern

Not everything should be saved.

Short one-off answers, low-value chit-chat, or unverified impressions do not need durable memory. The system aims for meaningful continuity, not transcript hoarding.

## Takeaway

Memory is not only storage. It is classification, routing, and later interpretation.
