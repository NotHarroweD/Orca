# Orca cheat sheet

One page. Print it, pin it, or keep it open next to your sessions.

## The loop

**Orchestrator** (most capable tier) writes the spec, **Implementer** (cheapest tier that works) builds it,
**Reviewer** (fresh session) audits it, and the findings go back to the orchestrator.
Then: fix, or move on.

## The six principles

1. **One outcome per spec.** If it feels big, split it.
2. **Specs carry the facts.** No hunting, no guessing.
3. **Tests first, and prove they can fail.** Break the code once to confirm the test notices.
4. **Define "done" mechanically.** A checklist, not a feeling.
5. **Never let the builder grade itself.** A fresh reviewer sees the result, not the summary.
6. **Fresh session per task, state in files.**

## Rhythm

- Plan the **whole project** up front. Write specs for the **next phase only**.
- After each phase: update `plan.md` and `decisions.md`, write `handoff.md`, then spec the next phase.
- Parallel tasks are specced together, and must not share files.

## A good spec has

Why · Allowed files · Task · Facts · Tests + breaks · Checks · Commit message · Report location · Out of scope

## Definition of done

- [ ] Every check passes (`./check`)
- [ ] Only allowed files changed
- [ ] No tests deleted, weakened, or skipped
- [ ] Working tree clean
- [ ] Commit message matches the spec
- [ ] Report saved to `docs/reports/`

## Session starters

- **Orchestrator:** "You are the orchestrator. Read AGENTS.md, then docs/handoff.md, docs/plan.md, docs/decisions.md."
- **Implementer:** "You are the implementer. Read AGENTS.md, then docs/specs/SPEC-XXX.md. Do exactly what it says."
- **Reviewer:** "You are the reviewer. Read AGENTS.md. Review SPEC-XXX against the result. Don't read the implementer's report. Find problems."

## Git

One branch per task · one commit per spec, exact message · reports and reviews committed separately · merge only after review passes

## When something fails

1. Write one sentence on the **cause** first.
2. Fix or split the **spec** (free).
3. Fresh session with the exact failure (cheap).
4. One tier up, for that task only (expensive).

| Symptom | Likely cause |
|---|---|
| Different results every run | Ambiguous spec |
| Many edits, no progress | Thrashing: stop, restart with the exact failing test |
| Tests pass, reviewer finds bugs | Weak tests: add breaks |
| Touches wrong files | Allowed-files list missing or loose |
| Fails every time | Task too big for this tier |

## Common mistakes

Specs too big · vague specs · skipping review · reviewing from the builder's report · parallel tasks sharing files ·
escalating the model instead of fixing the spec · continuing a long failing session · no single check command ·
forgetting to record decisions

## Learn more

[Guide](guide/README.md) · [Worked example](examples/inventory) · [AGENTS.md](AGENTS.md)
