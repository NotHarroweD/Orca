# Chapter 10: Measuring savings

**In one line:** track a few simple numbers so you know what the workflow is actually doing for you.

It's easy to feel like this works. It's more useful to know. A few numbers are enough.

## What to track, per task

| Field | Why it matters |
|---|---|
| Task ID | So you can compare tasks |
| Tier used by each role | To see where tokens go |
| Tokens used (per role, if you can see it) | The main cost |
| First-try pass? (yes/no) | The best single quality signal |
| Rework rounds | How many fixes before it was accepted |
| Defects the reviewer found | Whether review is earning its keep |
| Spec size | Relates to pass rate |

A spreadsheet is plenty. One row per task.

## What to look at

- **Tokens by role.** Is the orchestrator really a small share of the total?
- **First-try pass rate** over time. It should rise as your specs improve.
- **Pass rate vs. spec size.** Where does it start dropping? That's your size limit.
- **Defects found by review** on tasks that passed all checks. If it's ever zero across many tasks,
  your checks may be strong, or your reviewer may be too gentle.

## An A/B test you can run yourself

To test whether independent review is worth it:

1. Pick several comparable tasks.
2. For half, run the full loop including a fresh-session review.
3. For the other half, skip the review (or let the implementer check its own work).
4. Compare defects found later, rework needed, and total tokens.

Keep the tasks as similar as you can, and run enough of them that one odd result doesn't decide it.

## Be careful comparing

- **Change one thing at a time.** If you switch tiers and spec style together, you won't know which mattered.
- **Don't lump different setups together** in one average.
- **Separate infrastructure failures** (timeouts, rate limits) from real task failures, since they say nothing about your spec.
- **Bigger tasks fail more** for reasons beyond the model. Compare like with like.

## Do this

Make the spreadsheet. Fill it in for your next five tasks. Look for one thing you'd change.

**Next:** [Chapter 11: Wrapping up](11-wrapping-up.md)
