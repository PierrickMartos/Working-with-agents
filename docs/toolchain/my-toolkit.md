---
title: My toolkit
date: 2026-06-17
tags: [toolchain]
---

# My toolkit

A short list of tools that have earned a permanent spot in how I work with agents. None are magic on their own. Together they remove friction so the agent spends its budget on the actual problem.

## `/goal`: set an intent, let the agent iterate to it

`/goal` hands Claude or Codex a target to converge on, then lets it keep iterating until that target is reached instead of stopping after one pass. I use it when the outcome is clear but the path isn't: state the goal, let the agent close the gap, then check the result against the goal.

## rtk: save tokens on routine commands

[rtk](https://github.com/rtk-ai/rtk) rewrites common dev commands into token-cheaper equivalents. It's not magic, but it trims the output the agent has to read for routine operations, which leaves more room for the work that matters. The principle it represents: shrink the cost of the boring stuff so the budget goes to the thinking.

## fff: fast search on large codebases

[fff](https://github.com/dmtrKovalenko/fff) is a fast file and content finder. On a big codebase the speed-up is real: the agent locates code in one quick call instead of grinding through slow searches. The bigger the repo, the more it pays off.

## Plannotator: a tighter feedback loop on plans

[Plannotator](https://github.com/backnotprop/plannotator) opens a review-and-annotate loop on a plan before any code gets written. I mark up the plan in place, catch wrong turns early, and hand the corrections back. It's far cheaper to fix a plan than the code it would have produced.

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/a_AT7cEN_9I" title="Plannotator demo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
