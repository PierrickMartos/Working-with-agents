---
title: Skills
date: 2026-06-17
tags: [toolchain, skills]
---

# Skills

Skills are my favorite agent tooling invention so far. A skill is a reusable, named workflow the agent loads on demand. Instead of re-explaining "here's how I write a weekly update" every time, that procedure lives in a skill and the agent reaches for it when it's relevant. The idea isn't tied to any one agent: it shows up across Claude Code, Codex, and others.

## Why I rate them above MCP

The whole appeal is how light they are. A skill is mostly just instructions, and it only enters the context when the agent actually needs it. An MCP server, by contrast, has historically meant loading tool definitions up front, which costs context whether or not you use them.

That gap is narrowing, to be fair. Harnesses have gotten better at not loading every tool eagerly, and MCP implementations are improving their token footprint too. But skills still win on lightness today, and lightness is what lets you stack a lot of them without drowning the context window.

## Light does not mean limited

The easy misread is that lightweight means low-power. It doesn't. A skill can bundle scripts and call out to real tooling, so you get the leverage of code without paying the standing context cost of an always-loaded integration. You reach for the heavy machinery only when the skill runs.

## What makes a skill work

- **Discovered, not memorized.** A good description means the agent picks it up at the right moment without me naming it.
- **Composable.** A thin personal command can wrap a generic skill and inject my context, so shared logic stays in one place.
- **Context-cheap.** The detailed procedure loads only when needed, not on every turn.
