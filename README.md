# Alchemy

Internal tool for website discovery, auditing, and migration. Built as a suite of single-file HTML tools running inside a shared shell.

Live: **https://libertymoose.github.io/Alchemy/**

---

## What it is

A set of tools that covers the full website production and migration pipeline — from initial audit through to redirect mapping and launch. Each tool handles one stage; together they form a workflow.

```
Foundry  →  Scout  →  Canopy  →  Atlas  →  Forge  →  Waypoint  →  Warden
 Setup      Audit    Structure   Content   New IA    Redirects     Launch
                                                                      ↓
                                                                   Charter
```

---

## Tools

| | Tool | Status | Purpose |
|---|---|---|---|
| ⛺ | Foundry | Live | Project hub — create a project, run the shared crawl, track pipeline progress |
| 🔍 | Scout | Live | Website audit — performance, security, SEO, content |
| 🌿 | Canopy | Live | Site structure — visualise and annotate a site's URL tree |
| 🗺️ | Atlas | Live | Content inventory — catalogue pages, assign dispositions (keep/redirect/delete etc.) |
| 🧭 | Waypoint | Live | Redirect mapping — build and validate old→new URL mappings |
| 🔨 | Forge | Concept | IA design — plan the new site structure |
| 🛡 | Warden | Concept | Launch validation — pre/post-launch checks |
| ⛵ | Charter | Concept | Roadmap planning — hour-budgeted task grid |

---

## Architecture

**No build process.** Every tool is a single `.html` file with all CSS and JS inline.

**No standalone mode.** Tools only run inside the Alchemy shell (`index.html`). The shell fetches a tool's HTML, strips its chrome, injects it into `#tool-mount`, and calls `window.ToolName.init(activeProject)`.

**Repo structure:**
```
Alchemy/
├── index.html        ← Shell (topbar, sidebar, Foundry pages)
├── Scout/index.html
├── Canopy/index.html
├── Waypoint/index.html
├── Atlas/index.html
└── home/index.html   ← Suite landing page
```

---

## Cloudflare Workers
Six Workers handle anything that can't run in the browser.

| Worker | Purpose |
|---|---|
| `foundrystore` | Project storage — KV-backed, used for share links and cross-device access |
| `scoutproxy` | Fetch proxy — returns `{ ok, status, headers, html }` for audited URLs |
| `scoutai` | Anthropic API proxy (AI drafts) + Google PSI proxy |
| `waypointspider` | Crawl proxy — used by Foundry, Canopy, and Waypoint |
| `waypointstore` | Waypoint session storage / share links |
| `canopystore` | Canopy session storage / share links |

---

## Design

IBM Plex Mono + IBM Plex Sans. Teal accent (`#008080`). Dark/light mode. No external dependencies beyond Google Fonts.
