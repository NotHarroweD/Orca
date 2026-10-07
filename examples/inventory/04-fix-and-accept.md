# Fix and accept

## The orchestrator's decision
The failure traces to the implementation, not the spec: the spec already demanded "leave the inventory exactly as it was"
and named a test for it. So no spec rewrite. Send it back with the exact failures.

## Fix prompt (fresh implementer session; no history from attempt 1)

> You are the implementer. Read AGENTS.md and docs/specs/SPEC-003.md.
> A review found two problems with an earlier attempt:
> 1. `Inventory.add` fills the existing stack before checking whether the remainder fits. If it doesn't fit,
>    the error is raised but the stack has already changed. Check capacity first (or roll back).
> 2. `test_full_inventory_raises` must also assert that `stacks` equals its value from before the call.
> Fix both, re-run the spec's breaks (the rollback break must now make a test fail), and report in the standard format.

## Second implementer report (excerpt)

```
STATUS: COMPLETE
BREAKS:
  | break                     | test that failed           | code restored |
  | MAX_STACK changed to 100  | test_overflow_splits_stack  | yes           |
  | rollback removed          | test_full_inventory_raises  | yes           |
```

Both breaks now make tests fail.

## Second review
VERDICT: PASS. The reviewer reproduced the earlier overflow case (stack stays at 60), tried both breaks,
and confirmed the tests catch them.

## The record
Added to `docs/decisions.md`:

> - `Inventory.add` is all-or-nothing: if it can't place everything, it changes nothing.

Added to the orchestrator's notes for future specs: *when a spec says "change nothing on failure," name the test
that checks it and require a break that proves the test works.*

## What this example shows
- Checks passing was not enough. The first attempt was wrong in a way no test noticed.
- The weak spot was visible in the implementer's own breaks table, but only the independent review acted on it.
- The fix was cheap: a fresh session, two numbered problems, no rewrite.
- The lesson went back into the project's files, so future specs improve.
