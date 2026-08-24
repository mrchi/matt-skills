---
name: grill-with-docs
description: A relentless interview to sharpen a plan or design, which also creates docs (ADR's and glossary) as we go.
disable-model-invocation: true
---

Call the Skill tool twice, for "grilling" and "domain-modeling".

## End of session

When the interview reaches a shared understanding and the user confirms it:

1. **Write the docs to disk now.** Every term resolved during the session goes into `CONTEXT.md` (use domain-modeling's format), and every decision that passed the three gates becomes an ADR under `docs/adr/`. Do not leave them in the conversation: the files are the deliverable.
2. **Stop there.** This skill produces documentation only. Do not write code, do not refactor, do not start implementation, and do not call `implement` or any other build step, unless the user explicitly asks you to.
