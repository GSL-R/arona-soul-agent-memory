# Example: Pre-Flight Leakage Case

This is a fictional example of an output-boundary failure.

## Failure

The agent writes a normal user response and accidentally appends an internal record payload:

```md
I updated the plan.

internal_record:
type: agent_lesson
body: remember to avoid false completion claims
```

## Why This Is Bad

The record payload did not belong in the user message.

It also gives the model a new pattern to repeat later. Once internal strings appear in normal conversation, they can become part of the agent's conversational style.

## Corrected Response

```md
I updated the plan and kept the persistence status explicit.
```

If a real record needed to be saved, the storage operation should happen through the actual memory tool, not by printing the payload in chat.

## Lesson

A pre-flight check is not just about polish.
It prevents internal structure from becoming user-facing behavior.

