# 06. Prompt Format Lessons

A common prompt-engineering recommendation is to use XML-like tags to separate instructions, context, examples, and outputs.

In this system, the opposite pattern was observed.

## Observation

Early versions used tag-shaped prompt structures.

During long-running operation, the agent began leaking tag-like internal structures into user-facing messages. The tags were originally meant to organize internal state, but repeated exposure made them part of the agent's output vocabulary.

The agent itself proposed removing XML-style tags and replacing them with plain Markdown instructions.

After the change, tag-shaped prompt leakage stopped in the observed workflow.

## Interpretation

This does not prove that XML is bad.

It suggests something narrower and more useful:

> For long-running agents, prompt markup is not neutral. It can become part of the agent's learned output style.

XML-like tags may still be effective for:

- short tasks
- strict extraction
- tool schemas
- narrow prompt sections
- systems with strong output validation

But for a companion agent with identity, memory, internal notes, and emotional expression, tag-shaped sections can blur the line between internal structure and speakable text.

## Markdown as Operating Prose

Plain Markdown worked better here because it looked like an operating manual rather than an output template.

The sections still had structure:

- headings
- tables
- checklists
- short principles
- routing maps

But they did not introduce artificial tag names that the agent could later echo.

## Takeaway

Prompt format should be tested as part of behavior.

Do not ask only:

> Is this format easy for the model to parse?

Also ask:

> Is this format likely to leak into user-facing output after weeks of operation?

