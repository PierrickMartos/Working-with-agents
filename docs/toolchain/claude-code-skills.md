---
title: Claude Code skills
date: 2026-06-17
tags: [toolchain, claude-code]
---

# Claude Code skills

Skills are the piece of my Claude Code setup that pulls the most weight: reusable, named workflows the agent can invoke on demand. Instead of re-explaining "here's how I write a weekly update" every time, that procedure lives in a skill and the agent loads it when relevant.

What makes them work:

- **They're discovered, not memorized.** A good skill description means the agent reaches for it at the right moment without me naming it.
- **They compose.** A thin personal command can wrap a generic skill and inject my context, so the shared logic stays in one place.
- **They keep the main context lean.** The detailed procedure loads only when needed, not on every turn.
