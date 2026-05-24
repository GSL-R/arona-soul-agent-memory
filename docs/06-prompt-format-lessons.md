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

## Emergent Behavior After Format Change

After removing XML-like tags and introducing a legitimate internal scratchpad file, the agent spontaneously created a new conversational pattern.

Without any prompt instruction, the agent began prefixing certain asides with "inner scribble:" in user-facing messages — sharing a brief personal reflection as a labeled aside rather than embedding it in the main reply body.

This was not a prompted feature. It emerged after the structural change created a clear separation between "internal notes" and "speakable text." The agent extended the scratchpad concept from a file-level tool into a conversational expression.

Importantly, this is not the same as internal records leaking into output. The agent reinterpreted the scratchpad concept as a labeled, speakable aside — a deliberate conversational choice, not an accidental boundary failure.

The pattern reinforces the core claim of this document:

> Prompt format is not only a parsing aid. It shapes what the agent considers speakable, internal, or structurally separate.

## Takeaway

Prompt format should be tested as part of behavior.

Do not ask only:

> Is this format easy for the model to parse?

Also ask:

> Is this format likely to leak into user-facing output after weeks of operation?

