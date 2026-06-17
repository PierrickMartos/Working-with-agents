# Working with Agents — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Scaffold the public `Working-with-agents` knowledge-base repo: README, CC BY 4.0 license, a `docs/` content tree with section indexes and one real starter note each, a curated links page, and a dormant MkDocs Material config that is proven site-ready.

**Architecture:** Markdown-first. All content lives under `docs/` (MkDocs' default content dir) so enabling the published site later is a switch-flip, not a file move. `mkdocs.yml` is committed but no site is built and no CI/deps are added to the repo. Site-readiness is verified once with an ephemeral `uvx` build that touches nothing committed.

**Tech Stack:** Markdown, YAML frontmatter, MkDocs Material (config only, dormant), git, `gh`/`git` for push. Ephemeral `uv`/`uvx` for one-time build verification.

## Global Constraints

- Repo: `PierrickMartos/Working-with-agents` (public), cloned at `~/Personal/Working-with-agents`.
- Voice: BLUF, concise, contractions. No em dashes, en dashes, or double hyphens. Use commas, periods, colons, new sentences. English, CEFR B2/C1.
- Every content note starts with YAML frontmatter: `title`, `date`, `tags`.
- No Node/Python dependencies, no `requirements.txt`, no CI workflow committed at this stage.
- License: CC BY 4.0 (replaces the repo's initial MIT `LICENSE`).
- GitHub About description (set on push): `Practical field notes on agentic coding: principles, toolchain, and workflows that hold up in real work.`
- Starter notes are editable drafts: real content, but Pierrick edits before they are final.
- Every `.md` file referenced by the site must appear in `mkdocs.yml` nav so `mkdocs build --strict` passes.

---

### Task 1: License + README landing page

**Files:**
- Modify: `~/Personal/Working-with-agents/LICENSE` (replace MIT with CC BY 4.0)
- Modify: `~/Personal/Working-with-agents/README.md` (replace 21-byte stub)

**Interfaces:**
- Produces: a README whose structure (the four sections + site note) is mirrored by `docs/index.md` in Task 2 and by `mkdocs.yml` nav in Task 5.

- [ ] **Step 1: Replace the LICENSE with CC BY 4.0**

Fetch the canonical legalcode and write it verbatim to `LICENSE`:

```bash
cd ~/Personal/Working-with-agents
curl -fsSL https://creativecommons.org/licenses/by/4.0/legalcode.txt -o LICENSE
```

Verify it starts with the CC BY 4.0 header:

```bash
head -n 3 LICENSE
```

Expected: text beginning with `Creative Commons Attribution 4.0 International` (or `Attribution 4.0 International` followed by the license body). If `curl` fails (offline), paste the full CC BY 4.0 legalcode text manually.

- [ ] **Step 2: Write the README**

Overwrite `README.md` with:

```markdown
# Working with Agents

Practical field notes on agentic coding: principles, toolchain, and workflows that hold up in real work.

This is a living, working knowledge base, not a textbook. It's what I've learned using AI coding agents day to day as an engineering leader. Expect it to grow and change as the field does.

## What's here

- **[Learnings](docs/learnings/)** — distilled principles, mental models, and dos and don'ts for working with agents.
- **[Toolchain](docs/toolchain/)** — the tools I lean on (Claude Code, skills, MCP, hooks) and how I actually use them.
- **[Workflows](docs/workflows/)** — reusable patterns: how I structure a session, run TDD with an agent, and orchestrate work.
- **[Links](docs/links.md)** — an annotated reading list worth keeping.

## How it's organized

Everything is plain markdown under `docs/`, readable right here on GitHub. The structure is also MkDocs Material ready: a published site can be turned on later without moving a single file.

## License

Content is licensed under [CC BY 4.0](LICENSE). Use it, share it, build on it, with attribution.
```

- [ ] **Step 3: Verify the files**

```bash
cd ~/Personal/Working-with-agents
test -s LICENSE && grep -qi "Attribution 4.0 International" LICENSE && echo "LICENSE ok"
grep -q "Working with Agents" README.md && echo "README ok"
```

Expected: `LICENSE ok` and `README ok`.

- [ ] **Step 4: Commit**

```bash
cd ~/Personal/Working-with-agents
git add LICENSE README.md
git commit -m "docs: add README and switch license to CC BY 4.0"
```

---

### Task 2: Site home + section index pages

**Files:**
- Create: `~/Personal/Working-with-agents/docs/index.md`
- Create: `~/Personal/Working-with-agents/docs/learnings/index.md`
- Create: `~/Personal/Working-with-agents/docs/toolchain/index.md`
- Create: `~/Personal/Working-with-agents/docs/workflows/index.md`

**Interfaces:**
- Consumes: the four-section framing from the README (Task 1).
- Produces: section landing pages referenced by `mkdocs.yml` nav (Task 5). Each section index links to its starter note created in Task 3/4 using the exact filenames: `learnings/agent-as-senior-peer.md`, `toolchain/claude-code-skills-and-rtk.md`, `workflows/tdd-with-agents.md`.

- [ ] **Step 1: Write `docs/index.md`**

```markdown
---
title: Working with Agents
date: 2026-06-17
tags: [home]
---

# Working with Agents

Practical field notes on agentic coding: principles, toolchain, and workflows that hold up in real work.

This is a living, working knowledge base, not a textbook. It's what I've learned using AI coding agents day to day as an engineering leader. Expect it to grow and change as the field does.

## Sections

- **[Learnings](learnings/index.md)** — distilled principles, mental models, dos and don'ts.
- **[Toolchain](toolchain/index.md)** — the tools I lean on and how I use them.
- **[Workflows](workflows/index.md)** — reusable patterns for working with agents.
- **[Links](links.md)** — an annotated reading list.
```

- [ ] **Step 2: Write `docs/learnings/index.md`**

```markdown
---
title: Learnings
date: 2026-06-17
tags: [learnings]
---

# Learnings

Distilled principles, mental models, and dos and don'ts for working with AI coding agents. Short, opinionated, and earned in practice.

## Notes

- [Treat the agent as a senior peer](agent-as-senior-peer.md)
```

- [ ] **Step 3: Write `docs/toolchain/index.md`**

```markdown
---
title: Toolchain
date: 2026-06-17
tags: [toolchain]
---

# Toolchain

The tools I lean on when working with agents, and how I actually use them day to day. Less "what exists", more "what earns its place".

## Notes

- [Claude Code skills and RTK](claude-code-skills-and-rtk.md)
```

- [ ] **Step 4: Write `docs/workflows/index.md`**

```markdown
---
title: Workflows
date: 2026-06-17
tags: [workflows]
---

# Workflows

Reusable patterns for getting real work done with agents: how I structure a session, keep quality high, and orchestrate larger tasks.

## Notes

- [TDD with agents](tdd-with-agents.md)
```

- [ ] **Step 5: Verify the files**

```bash
cd ~/Personal/Working-with-agents
for f in docs/index.md docs/learnings/index.md docs/toolchain/index.md docs/workflows/index.md; do
  head -n 1 "$f" | grep -q '^---$' && echo "$f frontmatter ok" || echo "$f MISSING frontmatter"
done
```

Expected: four `... frontmatter ok` lines.

- [ ] **Step 6: Commit**

```bash
cd ~/Personal/Working-with-agents
git add docs/index.md docs/learnings/index.md docs/toolchain/index.md docs/workflows/index.md
git commit -m "docs: add site home and section index pages"
```

---

### Task 3: Starter notes (learnings, toolchain, workflows)

**Files:**
- Create: `~/Personal/Working-with-agents/docs/learnings/agent-as-senior-peer.md`
- Create: `~/Personal/Working-with-agents/docs/toolchain/claude-code-skills-and-rtk.md`
- Create: `~/Personal/Working-with-agents/docs/workflows/tdd-with-agents.md`

**Interfaces:**
- Consumes: section index links from Task 2 (filenames must match exactly).
- Produces: three content pages referenced by `mkdocs.yml` nav (Task 5).

- [ ] **Step 1: Write `docs/learnings/agent-as-senior-peer.md`**

```markdown
---
title: Treat the agent as a senior peer
date: 2026-06-17
tags: [learnings, mindset]
---

# Treat the agent as a senior peer

The most useful framing I've found: the agent is a capable, senior colleague, not an oracle and not a junior to micromanage.

## Why it matters

If you treat it as an oracle, you stop checking its work and ship its mistakes. If you treat it as a junior, you spell out every step and lose the leverage. The senior-peer framing keeps you in the right posture: delegate the path, stay accountable for the outcome.

## What it looks like in practice

- **Give it the goal and the constraints, not the keystrokes.** A peer figures out the how. Spell out success criteria instead.
- **Expect it to push back.** Ask for tradeoffs and disagreement. If it only ever agrees, you're prompting it wrong.
- **Verify, don't trust.** Senior peers are still wrong sometimes. Run the code, read the diff, check the claim.
- **Let it run when the path is clear.** Don't interrupt good momentum to confirm obvious steps.

## The trap

The failure mode is drifting between the two bad poles: rubber-stamping output when you're busy, then over-controlling when you get burned. Hold the peer framing steady and the quality stays predictable.
```

- [ ] **Step 2: Write `docs/toolchain/claude-code-skills-and-rtk.md`**

```markdown
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

The general principle it represents: **shrink the cost of the boring stuff so the budget goes to the thinking.**
```

- [ ] **Step 3: Write `docs/workflows/tdd-with-agents.md`**

```markdown
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
```

- [ ] **Step 4: Verify the files**

```bash
cd ~/Personal/Working-with-agents
for f in docs/learnings/agent-as-senior-peer.md docs/toolchain/claude-code-skills-and-rtk.md docs/workflows/tdd-with-agents.md; do
  head -n 1 "$f" | grep -q '^---$' && echo "$f ok" || echo "$f MISSING frontmatter"
done
```

Expected: three `... ok` lines.

- [ ] **Step 5: Check the voice constraint (no dashes)**

```bash
cd ~/Personal/Working-with-agents
grep -RnP '\x{2014}|\x{2013}|--' docs/ && echo "FOUND forbidden dashes" || echo "no forbidden dashes"
```

Expected: `no forbidden dashes`. If any are found, rewrite those lines with commas, colons, periods, or a new sentence.

- [ ] **Step 6: Commit**

```bash
cd ~/Personal/Working-with-agents
git add docs/learnings/agent-as-senior-peer.md docs/toolchain/claude-code-skills-and-rtk.md docs/workflows/tdd-with-agents.md
git commit -m "docs: add starter notes for learnings, toolchain, workflows"
```

---

### Task 4: Annotated links page

**Files:**
- Create: `~/Personal/Working-with-agents/docs/links.md`

**Interfaces:**
- Produces: a content page referenced by `mkdocs.yml` nav (Task 5).

- [ ] **Step 1: Write `docs/links.md`**

```markdown
---
title: Links
date: 2026-06-17
tags: [links, reading-list]
---

# Links

An annotated reading list on agents and agentic coding. Kept short on purpose: only what I'd actually point a colleague to.

## Foundations

- [Anthropic: Building effective agents](https://www.anthropic.com/research/building-effective-agents) — the clearest breakdown of agent patterns versus plain workflows. Start here.

## Practice

- (add as I go) — when a post, talk, or doc changes how I work, it lands here with one line on why.

> This page grows by subtraction as much as addition. If a link stops being the thing I'd recommend, it comes off.
```

- [ ] **Step 2: Verify the file**

```bash
cd ~/Personal/Working-with-agents
head -n 1 docs/links.md | grep -q '^---$' && echo "links.md ok" || echo "links.md MISSING frontmatter"
```

Expected: `links.md ok`.

- [ ] **Step 3: Commit**

```bash
cd ~/Personal/Working-with-agents
git add docs/links.md
git commit -m "docs: add annotated links page"
```

---

### Task 5: Dormant MkDocs config + .gitignore, proven site-ready

**Files:**
- Create: `~/Personal/Working-with-agents/mkdocs.yml`
- Create: `~/Personal/Working-with-agents/.gitignore`

**Interfaces:**
- Consumes: every content page from Tasks 2 to 4 (all must be listed in nav for `--strict` to pass).
- Produces: a validated `mkdocs.yml` that builds cleanly; no `site/` artifact is committed.

- [ ] **Step 1: Write `.gitignore`**

```gitignore
# MkDocs build output (site is built in CI later, never committed)
/site/

# Python / tooling caches that may appear during local builds
.cache/
__pycache__/
.venv/
```

- [ ] **Step 2: Write `mkdocs.yml`**

```yaml
site_name: Working with Agents
site_description: "Practical field notes on agentic coding: principles, toolchain, and workflows that hold up in real work."
site_author: Pierrick Martos
site_url: https://pierrickmartos.github.io/Working-with-agents/
repo_url: https://github.com/PierrickMartos/Working-with-agents
repo_name: PierrickMartos/Working-with-agents

theme:
  name: material
  palette:
    - scheme: default
      toggle:
        icon: material/weather-night
        name: Switch to dark mode
    - scheme: slate
      toggle:
        icon: material/weather-sunny
        name: Switch to light mode
  features:
    - navigation.sections
    - navigation.top
    - navigation.instant
    - search.suggest
    - content.code.copy

markdown_extensions:
  - admonition
  - toc:
      permalink: true
  - pymdownx.superfences

nav:
  - Home: index.md
  - Learnings:
      - Overview: learnings/index.md
      - Treat the agent as a senior peer: learnings/agent-as-senior-peer.md
  - Toolchain:
      - Overview: toolchain/index.md
      - Claude Code skills and RTK: toolchain/claude-code-skills-and-rtk.md
  - Workflows:
      - Overview: workflows/index.md
      - TDD with agents: workflows/tdd-with-agents.md
  - Links: links.md
```

- [ ] **Step 3: Verify the site builds cleanly (ephemeral, nothing committed)**

Run an isolated build with MkDocs Material pulled in just for this run. Output goes to a temp dir so no `site/` lands in the repo:

```bash
cd ~/Personal/Working-with-agents
uvx --with mkdocs-material --from mkdocs mkdocs build --strict --site-dir /tmp/wwa-build-check
```

Expected: ends with `INFO - Documentation built in ...` and exits 0, with no `WARNING` lines (because `--strict` turns warnings into a non-zero exit). Common failure: a page not listed in nav. If so, add it to `mkdocs.yml` nav and re-run.

Fallback if `uvx`/`uv` is unavailable: `pipx run --spec mkdocs-material mkdocs build --strict --site-dir /tmp/wwa-build-check`. If neither is installed, at minimum validate YAML syntax with `python3 -c "import yaml,sys; yaml.safe_load(open('mkdocs.yml'))" && echo "yaml ok"` and note that a full build check is pending.

- [ ] **Step 4: Confirm no build artifact was committed**

```bash
cd ~/Personal/Working-with-agents
test ! -d site && echo "no site/ in repo (good)"
git status -s
```

Expected: `no site/ in repo (good)`, and `git status` shows only `mkdocs.yml` and `.gitignore` as new.

- [ ] **Step 5: Commit**

```bash
cd ~/Personal/Working-with-agents
git add mkdocs.yml .gitignore
git commit -m "build: add dormant MkDocs Material config and .gitignore"
```

---

### Task 6: Push and set repo description

**Files:** none (remote operations only)

**Interfaces:**
- Consumes: all commits from Tasks 1 to 5.

- [ ] **Step 1: Push to origin**

```bash
cd ~/Personal/Working-with-agents
git push -u origin HEAD
```

Expected: branch pushed, tracking set. If the default branch differs (e.g. `master` vs `main`), push the current branch name as-is.

- [ ] **Step 2: Set the GitHub About description**

```bash
gh repo edit PierrickMartos/Working-with-agents \
  --description "Practical field notes on agentic coding: principles, toolchain, and workflows that hold up in real work."
```

Expected: command succeeds. If `gh` is not authenticated, run `gh auth status` and have Pierrick authenticate, or set the description manually in the GitHub UI.

- [ ] **Step 3: Verify the remote state**

```bash
gh repo view PierrickMartos/Working-with-agents --json description,visibility,defaultBranchRef \
  --jq '{description, visibility, default: .defaultBranchRef.name}'
```

Expected: description matches, `visibility` is `PUBLIC`.

---

## Notes for the implementer

- The published MkDocs site is intentionally **not** enabled in this plan. Turning it on later is a follow-up: add one GitHub Actions workflow (build + deploy to Pages) and enable Pages in repo settings. No content moves.
- Starter notes are real drafts, not placeholders, but Pierrick reviews and edits them before treating them as final.
- Keep commits small and per-task as written, so each is independently reviewable.
