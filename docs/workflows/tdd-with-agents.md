---
title: TDD with agents
date: 2026-06-17
tags: [workflows, testing, tdd]
---

# TDD with agents

Test-driven development gets better with an agent, not worse, because the test is how you keep an autonomous worker honest.

## The loop

1. **Define success as a failing test first.** Write or have the agent write the test, then confirm it fails for the right reason.
2. **Implement to green.** Let the agent write the minimal code to pass.
3. **Run the tests yourself.** Don't take "tests pass" on faith. See the output.
4. **Commit small.** One green step, one commit. Easy to review, easy to revert.

## Why it fits agents specifically

- **The test is an objective gate.** An agent can rationalize that code "looks correct". A failing-then-passing test can't be rationalized away.
- **It bounds the blast radius.** Small, tested increments mean a wrong turn costs one task, not a tangled afternoon.
- **It turns "done" into something checkable.** "Done" means the tests you agreed on are green, verified live, not asserted.

## The discipline that's easy to drop

The temptation is to let the agent skip straight to implementation because it's fast. That's exactly when bugs slip through. Write the test first even when, especially when, it feels like overkill.
