---
name: grill-with-docs
description: A relentless interview to sharpen a plan or design, which also creates docs (ADR's and glossary) as we go.
disable-model-invocation: true
---

Call the Skill tool twice, for "grilling" and "domain-modeling".

## End of session

This skill produces the paper trail only: `GLOSSARY.md` and ADRs. Once the interview reaches a shared understanding and the user confirms it, stop: do not write code, do not write a spec or tickets, do not refactor, do not start implementation, and do not call `implement`, `to-spec`, or any other build step, unless the user explicitly asks. The spec is a later, separate step (`/to-spec`), not part of this skill.
