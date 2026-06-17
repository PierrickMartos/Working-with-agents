# Design: `working-with-agents`

- **Date:** 2026-06-17
- **Author:** Pierrick Martos
- **Status:** Approved (brainstorming), pending implementation plan

## Summary

A public GitHub repository that serves as a living, practitioner's knowledge base on
working with AI coding agents and agentic coding. It is two things at once:

1. A **personal knowledge base** Pierrick adds to and references over time.
2. A **public-facing signal** of his expertise as an Eng Area Deputy working with AI tooling.

Content is markdown-first (readable raw on GitHub today) and structured so a
**MkDocs Material** site can be enabled later with zero reorganization.

## Goals

- Capture distilled learnings, toolchain notes, reusable workflows, and curated links.
- Stay low-friction to add to: write a markdown file, push, done.
- Read well for an external visitor landing cold (clear structure, polished README).
- Be site-ready: flipping on the published site requires adding one CI workflow and
  enabling Pages, never moving content.

## Non-Goals

- No published site on day one (dormant `mkdocs.yml` only).
- No build tooling, Node/Python dependencies, or CI workflow at creation time.
- Not a definitive textbook; these are field notes, expected to age and churn.

## Naming & metadata

- **Repo name:** `Working-with-agents` (public; capital W as created on GitHub).
- **Description (GitHub About):** "Practical field notes on agentic coding:
  principles, toolchain, and workflows that hold up in real work."
- **License:** **CC BY 4.0** (decided 2026-06-17). Fits a public notes/writing repo
  better than a code license: it covers prose and requires attribution. Implementation
  replaces the repo's initial MIT `LICENSE` with the CC BY 4.0 text.

## Repository structure

```
README.md                  # landing: what this is, how it's organized, links into docs/
docs/
  index.md                 # site home (mirrors README intro for MkDocs)
  learnings/               # distilled principles, mental models, dos & don'ts
    index.md
  toolchain/               # Claude Code, skills, MCP, hooks, RTK — what they are + how I use them
    index.md
  workflows/               # reusable patterns: session structure, TDD-with-agents, orchestration
    index.md
  links.md                 # annotated reading list
mkdocs.yml                 # committed but dormant; site builds when enabled
.gitignore
LICENSE                    # CC BY 4.0
docs/superpowers/specs/    # design + planning docs (this file)
```

Rationale for content living under `docs/`: it is MkDocs' default content directory,
so enabling the site later is a switch-flip, not a file move. GitHub renders everything
natively in the meantime.

## Conventions

- Every note is plain markdown with light YAML frontmatter:
  ```yaml
  ---
  title: <human title>
  date: YYYY-MM-DD
  tags: [tag1, tag2]
  ---
  ```
- Section `index.md` files explain the purpose of each section and index its notes.
- Writing voice: BLUF, concise, contractions, no em/en dashes or double hyphens.
  English, CEFR B2/C1.

## Seeding (day-one content)

Each section folder ships with a short `index.md` plus **one real starter note**, drawn
from Pierrick's actual setup, so the repo is not a hollow skeleton:

- `learnings/` — one principle note (e.g. "Treat the agent as a senior peer, not an oracle").
- `toolchain/` — one tool note (e.g. Claude Code skills + RTK: what they are, how used).
- `workflows/` — one pattern note (e.g. TDD with agents: write/verify tests first, loop to green).
- `links.md` — a small seeded annotated list.

Starter notes are drafts for Pierrick to edit before they are considered final.

## Site-later path

- `mkdocs.yml` committed now with MkDocs Material theme config, search, and nav, but
  no site is built.
- When publishing is desired: add one GitHub Actions workflow (`mkdocs gh-deploy` or
  build+deploy to Pages) and enable GitHub Pages on the repo. No content changes.

## Local + remote

- Local path: `~/Personal/Working-with-agents` (already cloned), its own git repo.
- Remote: `https://github.com/PierrickMartos/Working-with-agents.git` (already created,
  public). Currently holds a stub `README.md` and an MIT `LICENSE`.

## Success criteria

- Repo browsable and self-explanatory on GitHub from the README alone.
- Adding a new note is: create a markdown file in the right folder, push.
- Enabling the site later requires no content reorganization.
- Day-one content includes at least one substantive note per section.
