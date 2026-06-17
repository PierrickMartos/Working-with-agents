---
title: Challenge the plan, then simplify the code
date: 2026-06-17
tags: [workflows, review]
---

# Challenge the plan, then simplify the code

The cheapest bug to fix is the one you catch in the plan. The second cheapest is the one you catch right after writing the code. So I put a review gate at both points, and I lean on adversarial review to make those gates real instead of a rubber stamp.

## Challenge the plan first

Before any code gets written, I have a subagent adversarially review the plan: poke holes in it, surface unstated assumptions, find the blind spots. A fresh agent with a mandate to disagree catches structural problems that I, having just written the plan, am primed to miss. Fixing the approach here costs minutes. Fixing it after implementation costs a rewrite.

## Then challenge the implementation

Once the code exists, run the same adversarial review on the implementation. Does it actually do what the plan said? What breaks at the edges? Where did the agent take a shortcut it shouldn't have? Same idea as the plan review, aimed at the diff.

## Catch the rest, then cut

Two skills close out the loop:

- **`/review`** catches the remaining correctness issues the adversarial pass didn't, the smaller bugs and oversights.
- **`/simplify`** then strips the implementation back: less code, fewer moving parts, nothing speculative. Quality, not behavior.

The order matters. Challenge the design before you build it, challenge the build before you trust it, then review and simplify what survives. Each gate is cheap and each one catches a different class of mistake.
