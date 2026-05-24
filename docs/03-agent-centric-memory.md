# 03. Agent-Centric Memory

Most assistant memory is user-centric.

Examples:

- the user prefers concise answers
- the user likes a specific tool
- the user works on a certain project
- the user dislikes a certain tone

That is useful, but it is incomplete for long-running agents.

## Agent-Centric Memory

Agent-centric memory records what the agent needs to remember about itself:

- recurring mistakes
- output leakage risks
- operating promises
- successful recovery patterns
- preferred internal workflows
- constraints of the surrounding tool environment
- proposed improvements awaiting approval

This turns the agent from a stateless responder into a system with an operational history.

## Example Categories

| Category | Question |
| --- | --- |
| Identity | What role should I recover after a reset? |
| Integrity | What must I never claim without tool confirmation? |
| Routing | Which memory source should I trust first? |
| Self-correction | What previous behavior caused problems? |
| Evolution | What should be proposed, piloted, or rolled back? |

## Important Boundary

Agent-centric memory should not become uncontrolled self-modification.

The public ARONA_SOUL pattern uses an approval gate:

- the agent may notice a pattern
- the agent may propose a rule
- the agent may run it as a pilot only after approval
- the agent should preserve rollback paths
- durable constitution changes require explicit user approval

The point is reflective continuity, not autonomous drift.

## Takeaway

For long-running agents, memory should preserve both user context and agent operating context.

