# Working with Agents

A public, living knowledge base on working with AI coding agents: principles, toolchain, and workflows. It is markdown-first and published as a MkDocs Material site at https://pierrickmartos.github.io/Working-with-agents/.

It doubles as a personal knowledge base and a public-facing signal of the author's expertise. Author: Pierrick Martos, Senior Engineering Leader at Alan.

## Structure

```
README.md                 # GitHub landing: purpose blurb, preview image, link to the site
mkdocs.yml                # MkDocs Material config (the site source of truth)
assets/                   # README images (NOT part of the site build)
docs/                     # all published content
  index.md                # site home
  learnings/              # distilled principles, mental models, dos and don'ts
  toolchain/              # tools and how they're used
  workflows/              # reusable patterns
  links.md                # annotated reading list
  superpowers/            # planning docs (specs/plans) — gitignored, local only
.github/workflows/        # deploy.yml: build + deploy to Pages on push to main
```

## Voice

Match the author's voice. See the principles below; they are not optional.

- BLUF: lead with the point, then the detail.
- Concise, flowing prose. Contractions always. No corporate filler.
- **Never use em dashes, en dashes, or double hyphens.** Use commas, colons, periods, or a new sentence.
- English at CEFR B2/C1: common vocabulary, short clauses, no rare words or native-only idioms.
- First person. Opinionated and practitioner-flavored, not encyclopedic. These are field notes, not a textbook.

## Adding or editing a note

1. Create the markdown file in the right section under `docs/`.
2. Start it with YAML frontmatter:
   ```yaml
   ---
   title: <human title>
   date: YYYY-MM-DD
   tags: [tag1, tag2]
   ---
   ```
3. Add a link to it in that section's `index.md`.
4. Add it to the `nav:` in `mkdocs.yml`. Every page must be in `nav`, or the strict build fails.
5. Verify the build (see below), then commit. Keep commits small and scoped.

## Verifying before commit

The repo ships no dependencies. Build with an ephemeral runner:

```bash
pipx run --spec mkdocs-material mkdocs build --strict --site-dir /tmp/wwa-build-check
```

`--strict` turns broken links and out-of-nav pages into a failure, the same gate CI uses. Also check for forbidden dashes:

```bash
perl -ne 'next if /^-{3,}\s*$/; print "$ARGV:$.: $_" if /\x{2014}|\x{2013}/ || /[^-]--[^-]/' docs/**/*.md docs/*.md
```

## Deploy

Pushing to `main` triggers `.github/workflows/deploy.yml`, which builds with `mkdocs build --strict` and deploys via the official GitHub Pages actions. Pages source is set to "GitHub Actions". No build artifact is committed (`/site/` is gitignored).

## Conventions and gotchas

- `docs/superpowers/` holds brainstorming specs and implementation plans. It is gitignored and excluded from the site build. Keep it local.
- `assets/` is for README images only. Do not reference it from `docs/` pages.
- License is CC BY 4.0 (content license, not a code license).
- `mkdocs-material` is pinned to `>=9,<10` in CI because MkDocs 2.0 is flagged as backward-incompatible. Don't loosen that without checking.
