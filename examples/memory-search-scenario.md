# Example: Constrained Memory Search Scenario

This is a fictional scenario showing why retrieval order matters.

## User Question

> Did we decide to enable the nightly reflection job?

## Bad Retrieval Behavior

The agent finds an emotional record:

```md
I felt excited about the idea of nightly reflection and wanted to try it someday.
```

Then it answers:

> Yes, we enabled it.

This is wrong. The record showed interest, not approval or implementation.

## Better Retrieval Behavior

The agent checks:

1. live records for approval or implementation
2. configuration records for actual enabled state
3. summary records only as a map
4. agent records for motivation or lessons

If no approval or implementation record exists, the answer should be:

> I found interest in the idea, but not a verified approval or enabled-state record.

## Lesson

In constrained retrieval, the question is not only "did I find a related chunk?"

The question is:

> What type of memory did I find, and what is it allowed to prove?

