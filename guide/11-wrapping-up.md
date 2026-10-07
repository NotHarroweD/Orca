# Chapter 11: Wrapping up

**In one line:** keep state in files, keep sessions short, and avoid the handful of mistakes that sink most attempts.

## Handoffs

At the end of any orchestrator session, write `docs/handoff.md`:

- what's done,
- what's in progress,
- what's next,
- open questions and decisions needed.

The next session starts by reading it. You never need to carry anything in your head or in a chat.

## Keep sessions short

Long sessions accumulate history, and history causes drift. Prefer many short, focused sessions
that each start from files over one marathon that slowly loses the plot.

## Common mistakes

1. **Specs that are too big.** The most common cause of failure. Split them.
2. **Vague specs.** If a careful human would have to ask questions, answer them in the spec.
3. **Skipping review** because the checks passed. Checks catch what you thought of; review catches the rest.
4. **Reviewing from the builder's report** instead of from the result itself.
5. **Letting parallel tasks share files.** Merge pain follows.
6. **Escalating the model instead of fixing the spec.**
7. **Continuing a long, failing session** rather than starting fresh with the exact failure.
8. **No single check command.** Without one, "done" means whatever the implementer says it means.
9. **Forgetting to record decisions.** The same question gets answered differently each time.

## The whole loop on one page

1. Orchestrator reads `handoff.md`, `plan.md`, `decisions.md`.
2. Orchestrator writes the next spec(s).
3. Implementer(s) build in fresh sessions, tests first, with deliberate breaks.
4. Reviewer, in a fresh session, audits the result against the spec.
5. Orchestrator accepts, sends back, or rewrites the spec.
6. Record decisions, update the plan, write the handoff.
7. Repeat.

## Where to go next

- Run the loop on a real project. The first one is for learning; the second is where it pays off.
- Track your numbers (Chapter 10) and tune your spec size and tier choices.
- Adapt `AGENTS.md` to your own conventions once you know what you'd change.
- Share what you learn with the community.

## Do this

Pick your next real task, write the spec, and run the full loop once, start to finish.
