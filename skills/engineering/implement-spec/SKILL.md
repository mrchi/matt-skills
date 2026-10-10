---
name: implement-spec
description: "Implement the result of /to-spec and /to-tickets in code."
disable-model-invocation: true
---

You have been provided a spec. This spec should have tickets associated with it, describing how to implement the spec.

The issue tracker should have been provided to you. If not, tell the user to run `/setup-matt-pocock-skills`.

The goal is the entire spec implemented on a single **integration branch**, with every ticket resolved the way the issue tracker closes work.

The tickets are not a list of steps. They are a **task graph** with blocking relationships between them. This means there is always a **frontier** of tickets which are ready to be grabbed.

Communication to and from subagents should be sparse. Communicate primarily through **context pointers**: to the spec, tickets, research notes, and previous commits. Don't duplicate information already available via pointers.

**Implementer subagents** should be run in the background where possible for maximum concurrency.

## Steps

1. Read the spec and tickets to understand the task graph.

2. (optional) Use an **exploration subagent** to conduct any exploration required by the tickets - relevant codebase files or external documentation. Ensure the exploration subagent can save files - it should save its markdown notes in a directory outside the repo, accessible by all future subagents. This lets **implementer subagents** focus on implementation rather than exploration.

3. Prepare the integration branch in its own **integration worktree**, separate from the invoking checkout:
   - Inspect existing branches and worktrees first. For a new spec, create a branch and linked worktree with names identifying the spec, based on the repository's default branch unless the user specifies another base ref. Leave the invoking checkout's branch, HEAD, index and working files unchanged; do not import its uncommitted changes.
   - To continue the same spec, reuse its existing integration branch and separate worktree without resetting them. Check available session state: if another instance is active, stop; if occupancy is unclear, ask the user before reusing. This check is not an atomic lock; do not add lock files or an instance registry.
   - Ask the user to resolve branch or path collisions without overwriting or deleting existing resources. If an isolated integration worktree cannot be established, stop rather than fall back to the invoking checkout.
   - Run all subsequent orchestration, mergers, review and final verification against the integration worktree. Give subagents its path and branch as context pointers.
   - If the issue tracker closes work through PRs, or the user asks for one, open a draft PR after the first merge in step 5 (a branch with no commits ahead of the base branch can't open one), marked as closing the spec and tickets.

4. Use **implementer subagents** to implement each ticket, each in its own worktree on its own branch. Each implementer subagent:
   - confirms its worktree is based on the integration branch before starting, and resets onto it if not;
   - calls the Skill tool with `tdd` to build the ticket;
   - merges the integration branch tip into its own branch before reporting done

5. Once an **implementer subagent** completes, merge its work to the integration branch with a **merger subagent**.

6. If this changes the **frontier** of available tickets, kick off more **implementer subagents** to work on the new tickets. This allows for maximum concurrency.

7. Once all tickets are complete, call the Skill tool with exactly `mattpocock-skills:code-review` on the integration branch (never the bare `code-review`, which resolves to Claude Code's own built-in review). Fix all issues raised by the code review in a single **implementer subagent**, then run final verification in the integration worktree. Make required gitignored fixtures, database configuration and credentials available there; if verification remains unavailable, report it as blocked and stop before step 8. Skipped checks are not passes, and the invoking checkout is not a verification fallback.

8. If a draft PR exists, mark it ready for review. Otherwise, resolve each ticket the way the issue tracker closes work. Report the integration branch and worktree path.

9. Clean up only safely completed **implementer subagent** worktrees whose work is committed and integrated; preserve uncommitted or unmerged work. Retain the integration branch and worktree after success, failure or interruption, and report their location when stopping.
