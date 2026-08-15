# CLAUDE.md — AutoClip AI

This file provides context and conventions for AI assistants (Claude Code and others) working in this repository.

## Project Overview

| Field       | Value                                              |
|-------------|----------------------------------------------------|
| Name        | AutoClip AI — Content Producer Dashboard           |
| Description | Single-page dashboard for an AI content generation & auto-posting platform |
| License     | MIT                                                |
| Owner       | yanyannoodle34-debug                               |
| Repository  | https://github.com/yanyannoodle34-debug/LOCAL-OC   |
| Status      | Frontend mockup / prototype — no backend yet       |

The app is a **UI-only** mockup of an AI content producer. The visible feature set covers dashboard analytics, a content pipeline (kanban), trend analysis, account management, a post queue, safety & compliance controls, and an API payload preview. There is no backend, database, or persistence — all data on screen is hard-coded sample data.

## Repository Structure

```
LOCAL-OC/
├── CLAUDE.md          # This file
├── LICENSE            # MIT
├── README.md          # Short stub
├── .gitignore         # Standard Node / editor ignores
├── package.json       # Dev-server convenience script
└── index.html         # The entire single-page app (HTML + CSS + JS inline)
```

Everything is intentionally in one file — it's a static prototype. When splitting becomes worthwhile (real backend, real state, real routing), migrate to a proper bundler (Vite + React or similar) rather than adding piecemeal files.

## Tech Stack

| Concern       | Choice                                              |
|---------------|-----------------------------------------------------|
| Language      | HTML + inline JavaScript (no build step)            |
| Styling       | Tailwind CSS via CDN (`cdn.tailwindcss.com`)        |
| Charts        | Chart.js 4.4 via CDN                                |
| Icons         | Font Awesome 6.5 via CDN                            |
| Fonts         | Inter + JetBrains Mono via `@fontsource` CDN        |
| Package mgr   | npm (only for `serve`)                              |
| Runtime       | Any static file server / browser                    |

Because everything runs from CDNs, the file is fully self-contained — no build, no `node_modules` required to view the page (but `npx serve` avoids CORS quirks).

## Getting Started

Open the app directly in a browser:

```bash
# Simplest: just open the file
open index.html            # macOS
xdg-open index.html        # Linux
```

Or run a static dev server (recommended — some browsers restrict `file://`):

```bash
npm start
# → serves at http://localhost:5173
```

That's it — no dependencies to install, no build to run.

## App Architecture

The UI is a **7-tab single-page app** driven by a simple `switchTab(name)` JavaScript function that toggles a `.active` class on `.tab-content` elements. Tabs:

1. **Dashboard** — KPI cards, performance line chart, platform doughnut, activity feed, upcoming-posts preview
2. **Content Pipeline** — 5-column kanban (Ideas → Scripting → Generating → Review → Scheduled)
3. **Trend Analysis** — Trending hashtags, engagement heat bar chart, 24h momentum multi-line chart
4. **Account Manager** — Cards for connected creator accounts (TikTok / YT Shorts / IG Reels)
5. **Post Queue** — Vertical timeline of scheduled posts for the next 24h
6. **Safety & Compliance** — Compliance stats, active safety rules with toggles, recent audits
7. **API Payload** — JSON preview of the `POST /content/publish` request body with a copy button

Additional UI:
- **New Content modal** — opened by the top-bar `+ New Content` button; submits and jumps to Pipeline
- **Sticky header** — dynamic title + subtitle, search, notifications, primary action
- **Sidebar** — nav + live "System Online" mini-status card

### JavaScript layout (inside `index.html`)

- `tabMeta` — map of tab name → `[title, subtitle]` for the header
- `switchTab(name)` — toggles tab visibility + updates nav active state + header text
- `openCreateModal()` / `closeCreateModal()` / `submitCreate(e)` — modal wiring
- `copyPayload()` — copies the JSON block via `navigator.clipboard`
- Chart.js initializations for `performanceChart`, `platformChart`, `trendChart`, `momentumChart`

### Design system

Defined in the Tailwind config inside `<script>` at the top:

- **Color palette** — `dark-*` (slate scale), `brand-*` (indigo), `neon.*` (green/red/yellow/cyan/pink/orange)
- **Fonts** — `font-sans` = Inter, `font-mono` = JetBrains Mono
- **Utility classes in `<style>`** — `.glass`, `.glass-card`, `.glow`, `.pulse-dot`, `.slide-in`, `.tab-active`, `.hover-lift`, `.kanban-col`, `.timeline-line`, `.modal-backdrop`

Preserve the glass-morphism dark aesthetic when extending — matching cards should use `.glass-card rounded-2xl p-5` and cards that hover should add `hover-lift`.

## Development Workflow

### Branches

- **`main`** — default; never push directly
- **`claude/<description>-<id>`** — AI-generated branches (currently `claude/claude-md-docs-1e0abr`)
- **Feature branches** — from `main`, use descriptive names

### Commits

Imperative-mood, concise:

```
feat: add trend momentum chart to Trends tab
fix: correct copy-button feedback timeout
docs: update CLAUDE.md for new stack
```

### Push

```bash
git push -u origin <branch-name>
```

### Pull Requests

Do not open one unless explicitly asked. If asked, check `.github/` for a PR template first.

## Code Conventions

- **No build step.** Keep everything runnable by opening `index.html` in a browser. If a build ever becomes necessary, migrate the whole file to a real toolchain in one commit — don't half-migrate.
- **Inline over external.** Since there is no bundler, keep new styles/scripts inline in `index.html` unless the file becomes unmanageable (>2500 lines).
- **Tailwind first.** Prefer Tailwind utility classes over custom CSS. Extend the config's `colors` / `fontFamily` if you need new tokens — do not sprinkle raw hex codes in markup.
- **Sample data.** All numbers, names, and activity items are placeholders. When adding new UI, keep the same fictional tone (@handles, plausible metrics, rounded percentages).
- **No emojis in code.** UI uses Font Awesome icons; source code stays emoji-free.
- **Comments.** Write no comment unless the WHY is non-obvious. Never explain WHAT the code does — the identifier names already do.

## Environment Variables

None. There is no backend and nothing to configure. If real API integrations are ever added:
- Store secrets in `.env` (already gitignored)
- Ship a `.env.example` with placeholders and a one-line comment per variable
- Document required variables in this file

## Testing

No tests yet. If tests are added:
- Frontend: Playwright or Vitest for the interactive pieces (`switchTab`, modal, `copyPayload`)
- Document how to run them here
- Add a `test` script in `package.json`

## AI Assistant Guidelines

### Do

- Preserve the glass-morphism dark visual language when editing
- Reuse existing utility classes (`.glass-card`, `.hover-lift`, `.pulse-dot`, etc.) rather than inventing new ones
- Keep the 7-tab structure and the `switchTab` pattern when adding new tabs
- Extend `tabMeta` when adding a tab so the header title updates correctly
- Commit and push to the designated branch after completing tasks

### Do not

- Push directly to `main`
- Open a pull request unless explicitly asked
- Add a build system, framework, or bundler without a very good reason (and if you do, migrate the whole file at once — do not fragment it)
- Introduce new dependencies without asking — everything is currently CDN-based on purpose
- Add features, refactoring, or abstractions beyond what the task requires
- Add comments explaining WHAT the code does
- Create additional README or documentation files unless explicitly asked (CLAUDE.md is the exception)
- Leave half-finished implementations

### When in doubt

Ask a clarifying question rather than making a large assumption about intent.
