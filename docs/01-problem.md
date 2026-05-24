# 01. Problem

Long-running companion agents have a different failure profile from short-lived task assistants.

A coding assistant can often succeed by reading the current repository, answering the current request, and discarding the rest. A companion-style agent needs continuity across days, resets, compacted sessions, tool failures, and changed model backends.

The hard part is not making the agent sound warm in one response. The hard part is making the agent recover:

- who it is supposed to be
- what promises it has made
- what mistakes it should not repeat
- what should be remembered about the user
- what should be remembered about itself
- which internal notes must not appear in user-facing output

## Design Question

How can an agent preserve continuity when memory retrieval is limited, imperfect, and external to the model's native context?

ARONA_SOUL answers this by treating the prompt as an operating constitution and the memory system as a routed archive rather than a raw transcript store.

## Non-Goals

This project is not trying to provide:

- a universal prompt template
- a perfect memory system
- a fully autonomous self-modifying agent
- a general benchmark for all prompt formats

It is a case study from an operated system.

## Key Observation

The agent's identity and behavior were more stable when the system separated:

- runtime tool rules
- persona and communication rules
- factual event records
- emotional/self-reflective records
- daily summaries
- proposed rule changes
- pre-flight output checks

The separation mattered more than the exact prose of any single rule.

