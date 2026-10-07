# Chapter 2: Choosing a stack

**In one line:** pick tools that give fast, automatic answers to "does this work?"

Orchestration only works if the implementer can check its own work and the reviewer can check it again.
That means your stack matters more than usual. A good stack for this workflow has these traits.

## What to look for

1. **Everything runs from the command line.** If a task can only be verified by clicking around in an editor,
   an agent can't verify it.
2. **One command runs all checks.** Tests, linting, and type checks should be a single command, such as `./check`.
   You'll reference it in every spec.
3. **Tests are fast.** If the suite takes ten minutes, agents will skip it or time out. Aim for seconds.
4. **It's popular and well documented.** Cheaper models know common tools well and stumble on obscure ones.
5. **It has few moving parts.** Every extra dependency is another way for a task to fail for reasons unrelated to the spec.
6. **Logic can be separated from presentation.** Code that doesn't depend on a window, a GPU, or a running engine
   is easy to test headlessly.

## Applying this to game development

Games make point 6 the big one. Rendering, audio, and input are hard to check automatically.
So structure the project in layers:

- **Core logic** (rules, inventory, combat math, save data): plain code, no engine calls, fully unit-tested.
- **Glue** (connecting logic to the engine): thin, and tested where possible.
- **Presentation** (visuals, sound, feel): reviewed by a human, since that's what you actually judge by eye.

Orchestrate the first two layers heavily. Keep the third closer to you.

## Our running example

An inventory system for a 2D game: add and remove items, stack limits, weight limits, and saving and loading.
We'll build the logic as a standalone library with its own tests, with no engine required.

## Questions to ask before committing to a stack

- Can I run the tests with no window and no manual steps?
- Can one command run every check?
- Would a model know this tool well without reading its docs?
- Is it simple enough that a failure points at the spec, not the setup?

## Do this

Write down your stack in one paragraph, then write the single command that runs all checks.
If you can't write that command yet, fix that first. We'll use it in every chapter from here.

**Next:** [Chapter 3: Setting up the repo](03-setting-up-the-repo.md)
