# Graduate Institute of Journalism, NTU — English Website

## Project Overview
Static one-page English website for the Graduate Institute of Journalism (新聞研究所) at National Taiwan University. Deployed on GitHub Pages at `https://ntujour-en.github.io/`.

The Chinese-language site at `https://ntujour.github.io/` serves as the visual design reference.  
English source content: `https://webpageprodvm.ntu.edu.tw/Journalism/Default.aspx`

## Tech Stack
- Plain HTML + CSS — no frameworks, no build tools
- Vanilla JavaScript (ES6+) for tab switching, scroll-spy, and AJAX data loading
- GitHub Pages (static hosting, `main` branch root)

## File Structure
```
index.html              Main single-page site
css/style.css           All styles
data/
  faculty.json          Faculty data for all six tabs
  news.json             News items list
faculty/                Individual full-time faculty profile pages
  adrian-rauchfleisch.html
  chen-ling-hung.html
  hui-ju-tsai.html
  i-i-chan.html
  ji-lung-hsieh.html
  lih-yun-lin.html
  lokman-tsui.html
image/                  Faculty photos and other images
LOG.md                  Prompt-by-prompt change log
CLAUDE.md               This file
.claude/worktrees/      Claude Code worktrees (not deployed)
```

## Page Layout (NHK-style)
| Zone | Class | Notes |
|------|-------|-------|
| Header | `.site-header` | 54 px, sticky, maroon |
| Sidebar | `.site-sidebar` | 210 px, sticky below header, left nav |
| Main | `.site-main` | flex-fill content area |
| Footer | `<footer>` | Full-width — must live **outside** `.site-layout` |

The `<footer>` sits outside `<div class="site-layout">` so it isn't constrained by the sidebar column.

## Faculty Section
Six tabs driven by JavaScript:

| Tab id | Label |
|--------|-------|
| `faculty-fulltime` | Full-Time |
| `faculty-adjunct` | Adjunct |
| `faculty-specialist` | Adjunct Specialist |
| `faculty-emeritus` | Prof. Emeritus |
| `faculty-joint` | Jointly Appointed |
| `faculty-remembrance` | In Remembrance |

- Data loaded at page-load via `fetch('data/faculty.json')`
- Cards: horizontal flex layout (photo left 110 px, info right)
- Grid: 2-column, `grid-auto-rows: 160px` for uniform height
- **Full-time cards**: `<a class="faculty-card" href="faculty/…">` — entire card clickable
- **Non-full-time cards**: `<div class="faculty-card">` — no hover lift, no name underline
- **Remembrance cards**: extra class `faculty-card-remembrance` (grey top border, reduced opacity)

## News Section
- Items loaded via `fetch('data/news.json')`
- To add/edit news: edit `data/news.json` only — no HTML changes needed
- Pinned items (`"pinned": true`) are sorted to the top automatically
- `tagClass` is **auto-derived** from `tag` in JavaScript — never add it to the JSON

## Color Scheme
```
--maroon:       #671919   (NTU brand, nav background)
--maroon-dark:  #3e0f0f   (footer background)
--gold:         #efa22a   (accent, active/hover)
```
Body font: Georgia (serif). UI font: -apple-system (sans-serif).

## Data JSON Schemas

### `data/news.json`
```json
[
  {
    "title": "Headline text",
    "date": "2025-05-08",
    "tag": "Forum",
    "excerpt": "One or two sentence summary.",
    "image": "news-photo.jpg",
    "pinned": true,
    "link": "https://..."
  }
]
```

| Field | Required | Notes |
|-------|----------|-------|
| `title` | ✅ | Headline |
| `date` | ✅ | `YYYY-MM-DD` — year is derived automatically |
| `tag` | ✅ | `Forum` / `Award` / `Event` / `Research` |
| `excerpt` | ✅ | Short summary (1–2 sentences) |
| `image` | optional | Filename inside `image/` folder |
| `pinned` | optional | `true` → pinned to top; omit if false |
| `link` | optional | External URL for "Read more" |

`tagClass` is **never written to the JSON** — it is derived from `tag` automatically by the JS renderer.

### `data/faculty.json`
```json
{
  "fulltime": [
    {
      "name": "English Name",
      "nameZh": "中文名",          // optional
      "title": "Professor",        // optional (badge text)
      "photo": "image/Name.jpg",
      "placeholder": "謝",         // optional (1-2 char fallback)
      "tags": ["Tag A", "Tag B"],
      "profileUrl": "faculty/name.html"  // fulltime only
    }
  ],
  "adjunct": [ … ],
  "specialist": [ … ],
  "emeritus": [ … ],
  "joint": [ … ],
  "remembrance": [ … ]      // cards get grey top border + reduced opacity
}
```

## Workflow: Adding or Editing a News Item

> No Skill needed — Claude follows these steps whenever the user says "新增貼文", "add news", "修改文章", etc.

### Step 1 — Field check
Identify which **required** fields the user hasn't provided and list them clearly.  
Example response:
> 你目前提供了標題和摘要，還缺少：**日期**（格式：YYYY-MM-DD）、**類別**（Forum / Award / Event / Research）。這樣就好，還是要補上？

### Step 2 — Confirm
Wait for the user to fill in the gaps **or** explicitly say "就這樣" / "proceed". Do not write until confirmed.

### Step 3 — Write to `data/news.json`
- For a new item: **prepend** it to the array (newest first)
- For editing: find the matching title and update in-place
- Rules:
  - Do **not** add `tagClass` — it is derived by JS
  - Omit `image`, `pinned`, `link` if not provided (don't write `null`/`false`)
  - `date` must be `YYYY-MM-DD`

### Step 4 — Commit
```bash
git add data/news.json
git commit -m "news: add/update '<short title>'"
```

### Step 5 — Preview (auto-open tab)
After committing, push and open the live site:
```bash
git push
```
Then open a browser tab to `https://ntujour.github.io/en/`:
- **If Chrome MCP is available**: use `mcp__Claude_in_Chrome__tabs_create_mcp` + `mcp__Claude_in_Chrome__navigate`
- **Fallback**: `open "https://ntujour.github.io/en/"` via Bash

---

## Development Workflow
- Working directory: `/Users/hebe/Desktop/web/ntujour-en.github.io/` (main branch)
- Worktree (legacy): `.claude/worktrees/agitated-hamilton-bceda0/` — sync with `cp` if used
- Commit to `main` branch directly; push to `origin` to deploy on GitHub Pages
- `LOG.md` records every prompt session (date, summary, files changed)
- GitHub Pages URL: `https://ntujour.github.io/en/`
