# Chapter 3: Setting up the repo

**In one line:** put everything an agent needs in files, so no session depends on memory.

## The layout

```
your-project/
├── AGENTS.md          The workflow rules (from the Orca repo)
├── check              One command that runs all checks
├── src/               Your code
├── tests/             Your tests
└── docs/
    ├── plan.md        Phases and tasks
    ├── specs/         One spec per task
    ├── reports/       One implementer report per task
    ├── reviews/       One review per task
    ├── decisions.md   Decisions that bind future work
    └── handoff.md     Where things stand
```

Every file in `docs/` exists so that a brand-new session can pick up exactly where the last one stopped.

## Step by step

1. **Create the repo** and commit an empty project skeleton.
2. **Add `AGENTS.md`** from the Orca repo. Don't edit it yet. Use it as is until you know what you'd change.
3. **Create the `check` command.** Even with no tests yet, it should run and pass. Commit it.
4. **Create the empty `docs/` files.** A heading and a sentence each is enough.
5. **Decide on branches.** The simplest rule: one branch per task, merged only after review passes.
6. **Decide on commit messages.** Short and consistent (for example, `feat(inventory): add stacking`).
   Specs will state the exact message, so consistency makes the history readable.

## Branches and commits

Agents need clear git rules, or they'll improvise. These are the defaults in `AGENTS.md`:

- **One branch per task**, named for it (`spec-003-stack-limits`). Nothing is committed straight to main.
- **One commit per spec**, with the exact message from the spec.
- **Reports and reviews are committed separately** (`docs: report for SPEC-003`), so the work commit stays clean
  and the working tree is clean when the reviewer arrives.
- **You merge after review passes.** Merging is a decision, so it stays with you or the orchestrator.

If you'd rather use other conventions, change them in `AGENTS.md` once, and every spec inherits them.

## Starting your sessions

You'll have three kinds of sessions, and each begins the same way: tell it its role.

- *"You are the orchestrator. Read AGENTS.md, then docs/handoff.md and docs/plan.md."*
- *"You are the implementer. Read AGENTS.md, then docs/specs/SPEC-001.md and do exactly that."*
- *"You are the reviewer. Read AGENTS.md, then review SPEC-001 against the result."*

Short, explicit, and always pointing at files.

## decisions.md

Keep an append-only list of choices that must hold for everything that follows ("items stack up to 99",
"weights are integers, in grams"). Specs quote the relevant lines so the implementer never has to guess.

## Do this

Set up the layout above, make sure `./check` runs, and commit. Then open a new orchestrator session
and ask it to read your files back to you. If it can describe the project from files alone, your setup works.

**Next:** [Chapter 4: Planning in phases](04-planning-in-phases.md)
