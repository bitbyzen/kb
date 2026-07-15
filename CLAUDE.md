# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Common Commands

```bash
# Activate the virtual environment (required before running mkdocs commands)
source .venv/bin/activate

# Start local dev server
mkdocs serve

# Build static site
mkdocs build

# Deploy to GitHub Pages manually
mkdocs gh-deploy
```

## Architecture

This is an English-only MkDocs static knowledge base deployed to GitHub Pages at `https://bitbyzen.github.io/kb/`.

**Key files:**
- `mkdocs.yml` — single source of truth for the entire site: theme, plugins, and nav
- `docs_dir: docs/en` — all content lives under `docs/en/`
- `requirements.txt` — pin-free dependencies; `mkdocs<2` keeps the site on MkDocs v1
- `overrides/main.html` — injects a "Last updated" date above page content (suppressed on index pages)
- `.github/workflows/deploy.yml` — builds and deploys on every push to `main`

**Nav structure:**
`mkdocs.yml` defines a single `nav:` block. The top level uses `navigation.tabs` (Home, Desktop Notes, Mobile Notes, Photo Gallery). Each tab has a section index page (`index.md`) so clicking the tab lands on the index rather than the first child page. App and tool names sit directly below the tab level, with pages listed flat under each — no Operations/Reference/Troubleshooting sub-categories. Sections collapse and expand on click (`navigation.sections` is not enabled). App/section names within each tab are sorted alphabetically, except `Misc` which always stays last. Pages within each app/section are also sorted alphabetically by their H1 title.

A nav section label does not need to match its folder name(s) — e.g. "Unreal Engine" maps to `ue/`, "Perplexity" maps to `perprexity/`, and "Claude" maps to pages split across both `claude-ai/` and `claude-code/`. Related apps can share one nav label while keeping separate folders on disk; when doing this, interleave their pages alphabetically by H1 title within the merged section rather than grouping by folder.

**Doc folder conventions:**
Content is organised as `docs/en/<section>/<app-or-topic>/<slug>.md`. There are no category subfolders (`operations`, `reference`, `troubleshooting` — these have been removed). Each app/topic folder has an `img/` subfolder for all image files. Reference images in Markdown as `img/<filename>` (relative path). `docs/en/desktop/` holds both consumer-app and dev-tool topics side by side (the former separate `apps/` and `dev/` folders were merged).

**Section index pages:**
Each top-level section has an `index.md` at its root (e.g. `docs/en/desktop/index.md`, `docs/en/mobiles/index.md`). These must be the first entry under their section in `mkdocs.yml`.

**Adding a new page:**
1. Create the Markdown file in the appropriate folder under `docs/en/`.
2. Add its path directly under the relevant app/tool name in `mkdocs.yml` — no category grouping needed.
3. Insert at the correct alphabetical position by H1 title, both within the app/section and among app/section names.
All steps are required — pages not listed in the nav produce a warning and are excluded from the built site.

## Writing Standards

The full style guide is at `style-guide-en.md` (project root — not published to the site). Key rules to follow automatically:

**File naming:** Use kebab-case derived from the H1 title. Start the filename with a verb. Always omit articles (a, an, the) and possessives (your). Keep it to 40 characters or fewer (excluding `.md`); drop other filler words (in, on, to, for, etc.) if still over the limit. Images in the `img/` folder must be named after the MD file (e.g. `install-gimp.md` → images named `install-gimp-01.webp`, `install-gimp-02.webp`). Example: `# Install GIMP on Windows` → `install-gimp.md`.

**Folder structure:** The `docs/en/` folder contains `apps/`, `dev/`, `mobiles/`, `photos/`, and `stylesheets/`. Always place new documents inside `docs/en/`. The `stylesheets/extra.css` file lives at `docs/en/stylesheets/extra.css`. Notable folder names: miscellaneous tools use `misc/` (not `utilities/`), Unreal Engine uses `ue/` (not `unreal-engine/`).

**Document title (H1):** Title case, starting with an imperative verb. Minor words lowercase: a, an, the, in, of, to, with, for, and, or, but. Exception: particles in phrasal verbs are capitalized — **Log In**, **Sign In**, **Set Up**, **Zoom In** (e.g. `# Log In to DSM`). Only "in" as a standalone preposition stays lowercase (e.g. `# Enable Vertical Tabs in Chrome`). Example: `# Set Up Claude Code in WSL2`. Omit the app or section name from the title — readers already know the context from the nav. Write `# Edit Face Texture`, not `# Edit Face Texture in VRoid Studio`.

**Headings:** One H1 per document (title only). Use H2 for major sections, H3 for subsections. Title case for H2 and H3 as well. For sequential steps, use `## Step 1: Install the Application` (colon, not em dash). For parallel alternatives, use `## Method 1: Best Terminal Solution` (not `Option N:` or plain `1.`).

**Authorship note:** Every document generated by Claude Code must include this line directly under the H1, before any body text:

> **Note:** This document was generated by Claude Code and has not been reviewed by a human. Please use it as a reference only.

**Tone:** Second person ("you"), imperative form for instructions, short sentences. No filler words: simply, just, easily, of course.

**Code blocks:** Always specify the language. Use inline code for filenames, commands, and paths in running text.

**Callouts:** Use `> **Note:**` for tips and `> **Warning:**` for irreversible or harmful actions.

**Lists:** Bullets for unordered items, numbered lists for sequential steps. Keep items parallel in structure.

**Punctuation:** Use standard English quotation marks (`"..."`) in English documents.

**UI navigation:** Use `→` (not `>`) to separate menu steps. Bold each item: **Settings** → **Pages**.

**Privacy:** Never include real personal or device-specific information in any document. Always replace with generic placeholders:

| Type | Placeholder |
|------|-------------|
| Local IP address | `192.168.x.x` |
| Windows username | `<username>` |
| PC name | `<YOUR-PC>` |
| NAS QuickConnect ID | `<YOUR-QUICKCONNECT-ID>` |
| Passwords / tokens | `<YOUR-PASSWORD>` |
| Folder or directory names | `<YOUR-FOLDER>` or omit |
| Any other personal ID | `<YOUR-VALUE>` |

**Folder structure:** Never disclose real folder or directory names in any document. If a path is essential to the explanation, replace every folder name with a generic placeholder (e.g. `<YOUR-FOLDER>\<YOUR-PROJECT>`). If the structure is not essential, omit it entirely.
