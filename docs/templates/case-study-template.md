# Case Study: <Title>

Use this template to convert a private operation episode into a public-safe design note.

Do not paste raw private prompts, diaries, local paths, automation commands, user profile records, credentials, or hidden runtime payloads into this file.

If exact wording seems important, paraphrase it and mark it as a paraphrase instead of quoting the private source directly.

## Context

Describe the operational setting at a high level.

Keep the scope general enough that it can be understood without private runtime details.

## Observed Problem

What happened?

Phrase this as an observed failure or pressure, not as a universal law.

## Why It Mattered

Why was this risky for a long-running agent?

Consider memory integrity, output boundary, safety, user trust, operational continuity, or self-governance.

## Root Cause

What design pressure or ambiguity likely caused the issue?

If the cause is uncertain, say so.

## Adopted Pattern

What rule, routing change, boundary, or workflow was introduced?

Describe the pattern without exposing private implementation details.

## Trade-offs

What cost or new risk did the pattern introduce?

Good case studies include the downside.

## Generalized Lesson

What can another agent designer learn from this?

Keep it portable, but avoid claiming it applies to every model or runtime.

## Not Included

List what was intentionally omitted from the public version.

Examples:

- raw private prompt text
- personal diary entries
- local paths
- automation commands
- credentials or tokens
- private user profile records
- hidden runtime payloads

## Review Checklist

- [ ] No raw private prompt text is included.
- [ ] Private-source wording has been paraphrased instead of quoted directly.
- [ ] No local paths, commands, credentials, or tool payloads are included.
- [ ] Personal context has been removed or generalized.
- [ ] Single-episode observations are phrased as observed patterns, not universal rules.
- [ ] The target document and related terminology are consistent with the repository.
- [ ] The boundary or remaining risk is stated explicitly.
