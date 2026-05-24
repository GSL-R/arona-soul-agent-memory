# 05. Safety Boundaries

Long-running agents often produce internal material:

- memory payloads
- anchors
- tool commands
- scratch notes
- status labels
- recovery instructions

If those structures leak into user-facing messages, two things happen.

First, the user sees internal implementation noise.
Second, the model may learn that these strings are valid conversational output and repeat them later.

## Boundary Rule

The public ARONA_SOUL pattern uses a simple rule:

> Internal records belong to tools or durable storage. User messages belong to the user.

This leads to several operational rules:

- do not print a memory payload as a substitute for saving it
- do not claim a record was saved before the storage tool succeeds
- do not expose internal anchors or command-shaped text in normal replies
- if a record fails, report the failure without dumping the payload

## No Tool, No Record

The phrase "No tool, no record" is central.

An agent may intend to remember something, but intent is not persistence. If the write operation did not occur, the agent should not say it has remembered or saved the event.

This matters because false memory is worse than missing memory. A future agent may rely on a claimed record that never existed.

## Pre-Flight Check

Before final output, the agent checks:

- Did I actually verify the thing I am about to claim?
- Did I mix internal record text into the user message?
- Did I expose an internal command, anchor, or payload?
- Did I treat a guess as a fact?
- Did I modify a rule without approval?

This is a behavioral checklist, not a security boundary by itself. The surrounding runtime should still sanitize, validate, and restrict tools.

## Takeaway

Prompt rules cannot replace runtime safety, but they can reduce recurring behavioral failures when paired with tool constraints.

