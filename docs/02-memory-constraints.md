# 02. Memory Constraints

The original system did not assume perfect recall.

It was designed around a constrained memory environment where files are indexed in relatively small chunks and retrieved through search. In that setting, the agent cannot simply "remember everything." It has to know where to look and what kind of memory to trust.

## Constraint Model

The design assumes:

- memory is stored outside the model context
- retrieval returns partial chunks, not entire life history
- similar daily events may be mixed together
- old records may contain outdated interpretations
- tool execution can fail
- a model session can be reset or replaced

These constraints shape the prompt.

## Design Response

The prompt includes explicit routes:

- use factual logs first when reconstructing events
- use emotional diaries only for affective context
- use summaries as maps, not as source-of-truth records
- use procedures for operational rules
- use pending observations before promoting long-term user profile facts

This is a practical response to retrieval ambiguity.

## Why Not Just Store More?

More memory can make retrieval worse if records are not typed.

If factual logs, feelings, todo items, user preferences, automation results, and self-reflection all live in the same undifferentiated memory space, search results become hard to interpret. The agent may retrieve a poetic reflection and treat it as a factual event log.

The routing system exists to prevent that.

## Takeaway

In constrained memory systems, the prompt should not only say "remember this."
It should define memory classes, trust levels, retrieval order, and promotion rules.

