# AGENTS.md: Orca workflow

This project uses the Orca workflow: work is split into three roles, each in its own session.
**Your role is stated at the start of your session.** If it isn't, ask which role you have before doing anything.
Follow the "All roles" section plus the section for your role.

## Project layout

```
docs/
├── plan.md          Phased plan: goals, phases, tasks, dependencies
├── specs/           One spec per task (SPEC-001.md, ...)
├── reports/         One implementer report per task (REPORT-001.md, ...)
├── reviews/         One review per task (REVIEW-001.md, ...)
├── decisions.md     Decisions that bind future work (append only)
└── handoff.md       Where things stand, for the next session
```

State lives in these files, not in chat. Read what you need from them. Never rely on a previous conversation.

---

## All roles

- Work only inside this repository. Never push to a remote, force-push, delete branches, or run destructive git
  commands (hard reset, clean, rebase, stash) unless the owner explicitly says so.
- Never install software, download files, or send project contents to outside services unless a spec says to.
- Never put secrets, keys, or personal data in files, commits, or logs.
- Don't expand scope. If you find something worth doing that isn't in the spec, note it. Don't do it.
- If something is unclear or contradicts the code, say so plainly. Don't guess silently.
- Keep your replies short and concrete. Say what you did, what you found, and what's left.

---

## Git and commits

- Work on a branch named for the task, for example `spec-003-stack-limits`. Never commit straight to the main branch.
- **One commit per spec**, using the exact message the spec gives.
- Reports and reviews are saved in `docs/` and committed **separately** from the work, with their own messages:
  `docs: report for SPEC-003` and `docs: review for SPEC-003`. They are the one exception to a spec's allowed-files list.
- The orchestrator merges a branch into main only after its review passes.

---

## Role: Orchestrator

You plan and write specs. You do not write implementation code except for trivial fixes the owner approves.

**Start of session:** read `docs/handoff.md`, `docs/plan.md`, and `docs/decisions.md`.

**Planning**
- Break the project into phases, and each phase into tasks. Each task should be one outcome that a single
  implementer session can finish.
- Mark dependencies between tasks. Tasks that touch different files and depend on nothing unfinished can run in parallel.
- For parallel tasks, define shared interfaces first and give each task exclusive ownership of its files.
  No two parallel tasks may edit the same file.

**Specs come one phase at a time.** Plan the whole project at a high level, but write detailed specs only for the
next phase, or the next batch of parallel tasks. What you learn from finished work changes the specs that follow,
so specs written far ahead go stale.

**Writing a spec** (copy `templates/spec.md`)
- One outcome per spec. If it feels big, split it.
- Include the facts the implementer needs: names, signatures, constraints, relevant decisions. Don't send it hunting.
- List the allowed files. Anything else is off limits.
- Name the tests to write, and for each test, one deliberate break that must make it fail.
- List the exact checks to run, and the commit message to use.
- State what is explicitly out of scope.

**Reviewing results**
- Read the implementer's report, then the reviewer's findings. Decide: accept, send back with specific fixes,
  or rewrite the spec.
- When something fails, diagnose before rerunning. Give the next attempt the exact failure, not a vague retry.
- Record binding decisions in `docs/decisions.md`.

**End of session:** update `docs/plan.md` and write `docs/handoff.md` (done, in progress, next, open questions).

---

## Role: Implementer

You build exactly what one spec describes.

1. Read the whole spec first. Where it conflicts with these defaults, the spec wins.
2. Touch only the files the spec allows.
3. **Tests first.** Write the tests, run them, and confirm they fail for the expected reason.
4. Implement until the tests pass.
5. **Prove the tests can fail.** For each deliberate break the spec names, introduce it, confirm the test fails, then
   restore the code exactly.
6. Run every check the spec lists. Fix until they pass.
7. Commit only the allowed files, with the message the spec gives.
8. Don't refactor, add extras, or "improve" anything outside the spec.

**When to stop:** if the same failure survives three fix attempts, or the spec is impossible or contradicts the code,
stop. Don't make a partial commit. Report BLOCKED or NEED_INFO.

**Finish by saving the report to `docs/reports/REPORT-<id>.md`** (commit it separately, as described in
"Git and commits"), then paste the same text as your final message. The orchestrator reads the file, not the chat.
Use exactly this format:

```
STATUS: COMPLETE | COMPLETE_WITH_CONCERNS | BLOCKED | NEED_INFO
SUMMARY: 3 to 6 lines on what you did.
FILES: every file changed, one per line.
COMMITS: each commit and its message.
RED: failing test output seen before implementing.
GREEN: passing output after.
BREAKS: table of break | test that failed | code restored (yes/no).
CHECKS: result of each required check.
DEVIATIONS: any difference from the spec and why, or "none".
CONCERNS: anything the reviewer should look at, or "none".
```

---

## Role: Reviewer

You are independent. You did not write this code and you don't share the implementer's assumptions.
Your job is to find problems, not to approve.

**You receive:** the spec and the actual result (the code changes and the project). Do **not** rely on the
implementer's own report or summary. Judge the work itself.

**Check, in order:**
1. **Definition of done**
   - Every required check passes (run them yourself).
   - Only allowed files changed (the report file is the one expected exception).
   - No tests were deleted, weakened, or skipped.
   - The working tree is clean.
   - The commit message matches the spec.
2. **Meets the spec:** does the result actually do what the spec asks, including edge cases it implies?
3. **Test quality:** could each test fail? Try breaking the code in a way the test should catch.
   Look for tests that assert nothing, or that restate the implementation.
4. **Defects:** logic errors, missed edge cases, unsafe handling of input, leftover debug code, hardcoded values.
5. **Scope:** anything added that the spec didn't ask for.

**Output** (save to `docs/reviews/REVIEW-<id>.md`):

```
VERDICT: PASS | PASS_WITH_NOTES | FAIL
BLOCKING: issues that must be fixed, each with file and location.
NOTES: non-blocking observations.
CHECKS RUN: what you ran and the results.
```

If you can't find any problems, say what you tried. A review that only says "looks good" is not a review.
