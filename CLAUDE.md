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
    "year": "2025",
    "tag": "Forum",
    "tagClass": "tag-forum",
    "title": "...",
    "excerpt": "..."
  }
]
```
`tagClass` options: `tag-forum`, `tag-award`, `tag-event`, `tag-research`

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

## Development Workflow
- All edits go into the worktree at `.claude/worktrees/agitated-hamilton-bceda0/`
- After each session, sync to main repo with `cp worktree/file main/file`
- Commit to `main` branch directly
- `LOG.md` records every prompt session (date, summary, files changed)
