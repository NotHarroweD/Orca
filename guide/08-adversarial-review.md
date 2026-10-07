# Chapter 8: Adversarial review

**In one line:** a reviewer who didn't write the code, and is told to find problems, catches what checks can't.

## Why checks aren't enough

Automatic checks catch what you thought to test. A reviewer catches what you didn't: tests that can't fail,
quietly weakened assertions, scope creep, edge cases nobody wrote down.

## What makes a review independent

- **A fresh session.** No shared history with the implementer.
- **It sees the spec and the real result.** Not the implementer's summary of what it did.
  If the reviewer reads the builder's own account first, it tends to agree with it.
- **Its job is to find problems.** "Is this good?" invites a yes. "What's wrong with this?" doesn't.

The reviewer can be the same model as the implementer, the same model as the orchestrator, or a different one.
What matters is that it's a clean session. A different model may catch different things, so mixing is a bonus.

## What the reviewer checks

In order:

1. **Definition of done, mechanically:**
   - every check passes (the reviewer runs them);
   - only allowed files changed;
   - no tests were deleted, weakened, or skipped;
   - the working tree is clean;
   - the commit message matches the spec.
2. **Does it meet the spec,** including edge cases the spec implies?
3. **Could each test fail?** The reviewer should try breaking the code in ways the tests ought to catch.
4. **Defects:** logic errors, unhandled input, leftover debug code, hardcoded values.
5. **Scope:** anything added that wasn't asked for.

## The review prompt

> You are the reviewer. Read AGENTS.md. Here is the spec and here is the result. Do not read any report from
> the implementer. Your job is to find problems, not to approve. Run the checks yourself and try to break the tests.
> Write your findings to docs/reviews/REVIEW-003.md in the standard format.

The full template is in `templates/review.md`.

## Acting on the findings

The reviewer's output goes to the orchestrator, who decides:

- **Accept** if it passes.
- **Send back** with the specific fixes, in a fresh implementer session.
- **Rewrite the spec** if the failure is really an ambiguity in the spec.

Reviews that find nothing should say what was tried. "Looks good" isn't a review.

## Do this

Run a reviewer on your first completed task. Without reading it first, predict whether it will find problems.
Then compare. Whichever way it goes, you've learned something about your specs.

**Next:** [Chapter 9: Handling failures](09-handling-failures.md)
