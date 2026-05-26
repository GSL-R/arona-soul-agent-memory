# Origin and Scope

This repository was not created to publish a private companion prompt.

It was created to distill the design pressures that appeared while turning a terminal-based agent into a long-running companion system.

The public version is therefore a fieldbook: a set of reusable observations about memory, continuity, output boundaries, and self-review loops. It is not a raw runtime dump, a drop-in prompt, or a complete automation framework.

## Why This Project Exists

The original goal was not to build a character chatbot.

The goal was to explore whether a personal agent could support three kinds of continuity at once:

- daily routine support and context-aware reminders
- lightweight operational assistance around a personal computing environment
- emotional continuity across ordinary conversations, resets, and scheduled interactions

That combination created pressure that a normal chat session could not handle well. The agent needed to remember not only user preferences, but also its own promises, mistakes, operating rules, recovery procedures, and unresolved work.

This is why the project became about agent-centric memory rather than only user-centric memory.

## Original Operating Context

The private system ran as a terminal-centered personal agent with scheduled loops, constrained memory retrieval, and tool-mediated record writes.

The important public assumptions are:

- memory retrieval was limited and chunked, not full free-form recall
- long-term continuity had to survive model and session resets
- scheduled agent loops could re-enter the workflow after time had passed
- user-facing responses, internal notes, and durable records needed clear separation
- successful persistence required runtime evidence, not just natural-language intent

The exact local environment, tool names, commands, paths, access model, and automation details are intentionally out of scope for this public repository.

## Design Pressures

Several recurring pressures shaped the public patterns:

- **Continuity across time.** The agent needed a way to recover role, context, and unfinished work after resets or scheduled re-entry.
- **Constrained memory search.** Short indexed chunks encouraged compact records, stable labels, and careful routing.
- **Fact and reflection separation.** Factual events and emotional or self-correction records had to remain related without becoming interchangeable.
- **Verified persistence.** The agent could not safely claim that something was remembered unless a durable write actually happened.
- **Self-correction memory.** Repeated mistakes needed to become retrievable lessons, not just one-off apologies.
- **Safe expression.** Strict suppression of all internal expression created pressure for accidental leakage, so bounded user-facing expression channels became useful.
- **Governed evolution.** Operating-rule changes needed human approval, trial periods, and rollback paths.

These pressures are the source material for the repository's memory architecture and live-operation lessons.

## Public Scope

This repository includes:

- sanitized architectural explanations
- generalized failure patterns
- public example prompts
- fictional examples of memory routing and boundary checks
- templates for turning private operation episodes into public-safe case studies

This repository intentionally excludes:

- raw private prompt text
- private diaries or personal records
- local paths, account names, host details, and access structure
- automation commands or executable internal payloads
- exact tool names used in private operation
- real memory anchors or private indexing keys
- credentials, tokens, and environment details

The public documents preserve the lesson, not the private implementation.

## How to Read the Repository

Read this repository as a design case study.

Start with the problem and constraints, then move to the memory architecture, safety boundaries, and live-operation lessons. The public prompt files are examples of the distilled pattern; they are not production safety controls by themselves.

For the shortest path:

1. `01-problem.md`
2. `02-memory-constraints.md`
3. `03-agent-centric-memory.md`
4. `04-record-routing.md`
5. `10-case-study-matrix.md`
6. `09-lessons-from-live-operation.md`

Before adapting any pattern, read `05-safety-boundaries.md` and `../SECURITY.md`.
