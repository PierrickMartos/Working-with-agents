---
title: Claude Code skills and RTK
date: 2026-06-17
tags: [toolchain, claude-code]
---

# Claude Code skills and RTK

Two pieces of my Claude Code setup that pull real weight: skills and a token-saving CLI proxy.

## Skills

Skills are reusable, named workflows the agent can invoke on demand. Instead of re-explaining "here's how I write a weekly update" every time, that procedure lives in a skill and the agent loads it when relevant.

What makes them work:

- **They're discovered, not memorized.** A good skill description means the agent reaches for it at the right moment without me naming it.
- **They compose.** A thin personal command can wrap a generic skill and inject my context, so the shared logic stays in one place.
- **They keep the main context lean.** The detailed procedure loads only when needed, not on every turn.

## RTK (a token-saving CLI proxy)

RTK is a proxy that rewrites common dev commands into token-optimized equivalents, cutting the output the agent has to read for routine operations like `git status` or builds. The win is indirect but real: less noise in context means more room for the actual problem, and lower cost per session.

The general principle it represents: shrink the cost of the boring stuff so the budget goes to the thinking.
