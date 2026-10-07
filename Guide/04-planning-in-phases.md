# Chapter 4: Planning in phases

**In one line:** break the project into slices small enough that one session can finish each one.

## Phases, then tasks

A **phase** is a milestone you can verify: something that works end to end, however small.
A **task** is one piece of a phase, sized so a single implementer session can complete it.

Plan in this order:

1. **Phase 0: skeleton.** The repo, the `check` command, and one passing placeholder test.
2. **Early phases: the thinnest working slice.** The simplest version of the whole feature.
3. **Later phases: depth.** Edge cases, limits, polish, and persistence.

Prefer vertical slices (a little of everything that works) over horizontal ones (all the data structures first,
then all the logic). Slices stay testable the whole way.

## Sizing a task

A task is the right size when:

- it has **one outcome** you can state in a sentence;
- it touches a **small number of files**;
- you can describe **how to verify it** with specific tests;
- a fresh session could finish it **without needing the rest of the project in its head**.

If you can't state the outcome in one sentence, split it. If a task needs a long explanation, split it.
A spec that's too big is the most common reason cheap implementers fail.

## Dependencies

For each task, note what must be finished first. Tasks with no unfinished dependencies and no shared files
can run in parallel (Chapter 7).

## Example plan

```
# Plan: Inventory system

## Phase 0: Skeleton
- T0.1 Project setup, `check` command, placeholder test

## Phase 1: Core inventory
- T1.1 Item and Inventory data types            (after T0.1)
- T1.2 Add and remove items                     (after T1.1)
- T1.3 Stack limits                             (after T1.2)
- T1.4 Weight limits                            (after T1.2)

## Phase 2: Persistence
- T2.1 Save inventory to a file                 (after T1.3, T1.4)
- T2.2 Load inventory from a file               (after T2.1)
```

T1.3 and T1.4 depend on the same thing but touch different rules, so they can run in parallel
as long as they own different files.

## Let the orchestrator do the planning

Describe your project, your stack, and the principles from this guide, and ask for a phased plan in this shape.
Then **read it and push back**. The plan is the most valuable thing your top-tier model produces.

## Do this

Get a phased plan for your own project into `docs/plan.md`. Check that every task passes the sizing test above.

**Next:** [Chapter 5: Writing a spec](05-writing-a-spec.md)
