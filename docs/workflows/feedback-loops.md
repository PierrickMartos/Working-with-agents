---
title: Feedback loops
date: 2026-06-17
tags: [workflows, testing, observability]
---

# Feedback loops

Feedback loops matter more to me than any other practice when working with agents. An agent moves fast and confidently in the wrong direction just as easily as the right one. A loop is what catches the wrong direction before it costs you. The more layers you have, and the faster each one runs, the more autonomy you can safely hand over.

I think about them as a stack, from closest to the code to closest to the outcome.

## Code correctness: tests

Unit, functional, and end-to-end tests validate that the code does what it should. This is the tightest, fastest loop and the foundation. See [TDD with agents](tdd-with-agents.md) for how I run it with an agent.

## Behavior in the running app: Chrome MCP

Tests prove the logic. They don't prove the thing actually works in a browser. A Chrome MCP lets the agent drive the real UI and check the functional, high-level behavior: did the page render, does the flow complete, is the result on screen.

## Safety in production: Sentry / Datadog MCP

Once a change ships, error and APM tooling (via a Sentry or Datadog MCP) confirms you didn't break anything live. The loop closes in production, where errors, latency, and regressions surface in the place that counts.

## Outcome over time: Amplitude / Segment / Metabase MCP

The slowest and most important loop. Product analytics (Amplitude, Segment, Metabase MCP) tell you whether the change actually moved the outcome you cared about. This is the loop you iterate and watch on, not just to avoid breaking things, but to know if the work mattered at all.

## The point

Each layer catches what the one before it can't. Tests miss UI breakage. UI checks miss production errors. Production health misses whether anyone benefited. Stack them and an agent can run a long way on its own, because every kind of mistake has something waiting to catch it.
