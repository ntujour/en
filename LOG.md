# Change Log — Graduate Institute of Journalism, NTU (English Website)

> **Rule:** Every time a prompt is used to revise the code, record the entry here with:
> `## [YYYY-MM-DD HH:MM TST] — Brief title`
> followed by the prompt summary and files changed.
> Time zone: Taiwan Standard Time (TST, UTC+8).

---

## [2026-05-07 ~15:20 TST] — Initial website build

**Prompt summary:**
> 「我現在想要架設一個一頁式的英文版網頁，其中文版網頁為：https://ntujour.github.io/ （視覺風格參考）。英文資訊請參考：https://webpageprodvm.ntu.edu.tw/Journalism/Default.aspx。這個頁面會有以下資訊：簡短的 Introduction、新聞所 news、新聞所教師（full-time 專任教師需額外有連結，建立一個新的頁面）」

**Actions taken:**
- Fetched content from `ntujour.github.io` and `webpageprodvm.ntu.edu.tw/Journalism/` to gather design references, English content, faculty info, and news items.
- Fetched all 7 full-time faculty profile pages from the NTU official site.
- Created `css/style.css` — full stylesheet with dark-blue NTU color scheme (initial draft, later revised).
- Created `index.html` — one-page site with: site banner, sticky nav, hero section, Introduction (with pillar cards and stats), News (5 cards), Faculty grid (7 cards).
- Created 7 faculty profile pages under `faculty/`:
  - `ji-lung-hsieh.html`
  - `lih-yun-lin.html`
  - `chen-ling-hung.html`
  - `adrian-rauchfleisch.html`
  - `hui-ju-tsai.html`
  - `i-i-chan.html`
  - `lokman-tsui.html`

**Files created:** `css/style.css`, `index.html`, `faculty/ji-lung-hsieh.html`, `faculty/lih-yun-lin.html`, `faculty/chen-ling-hung.html`, `faculty/adrian-rauchfleisch.html`, `faculty/hui-ju-tsai.html`, `faculty/i-i-chan.html`, `faculty/lokman-tsui.html`

---

## [2026-05-07 ~15:34 TST] — Color scheme & banner redesign to match ntujour.github.io

**Prompt summary:**
> 「我的配色要和 https://ntujour.github.io/ 的配色一模一樣！還有最頂端的 bar 也要一樣！」

**Actions taken:**
- Fetched raw HTML source of `ntujour.github.io` via `curl` to obtain exact class names and structure.
- Fetched `ntujour.github.io/css/site-common.css` to extract exact color values.
- Fetched `ntujour.github.io/js/load-banner.js` to understand dynamic banner rendering.
- Identified the correct color palette:
  - Nav background: `#671919` (maroon)
  - Active/hover nav text: `#efa22a` (gold)
  - Footer background: `#3e0f0f` (dark maroon)
  - Banner background: `#f5f5f5` (light gray) with decorative images
- Rewrote `css/style.css` completely with the new color variables and banner styles.
- Updated `index.html`: replaced dark-blue `.topbar` + `.navbar` with light-gray `.site-banner` + maroon `.site-nav`; moved 中文 language link into nav; fixed scroll-spy offset calculation.
- Updated all 7 faculty pages via Python batch script: replaced `.topbar` + `.navbar` blocks with the new `.site-banner` + `.site-nav` structure.

**Files modified:** `css/style.css`, `index.html`, `faculty/ji-lung-hsieh.html`, `faculty/lih-yun-lin.html`, `faculty/chen-ling-hung.html`, `faculty/adrian-rauchfleisch.html`, `faculty/hui-ju-tsai.html`, `faculty/i-i-chan.html`, `faculty/lokman-tsui.html`

---

## [2026-05-07 ~15:40 TST] — Project review and documentation

**Prompt summary:**
> 「Please review whole project, and save the record as INSTRUCTION.md, and generate another LOG.md used to record each operation. And note a rule on INSTRUCTION.md, each time when using prompt to revise the code, please record each prompt's date and time.」

**Actions taken:**
- Reviewed full project file structure and all source files.
- Created `INSTRUCTION.md` with: project overview, file structure, design system (colors, typography, layout), banner/nav spec, content update guide, deployment notes, external dependencies, and the logging rule.
- Created `LOG.md` (this file) with retrospective entries for all previous sessions and the logging rule explanation.

**Files created:** `INSTRUCTION.md`, `LOG.md`

---

## [2026-05-07 ~16:00 TST] — Expand Faculty section with additional categories

**Prompt summary:**
> 「請幫我修改 index.html，我希望在 faculty 的階段，可以將標題「Full-Time Faculty」放大一點，且接續幫我加上 adjunct faculty, adjunct specialist faculty, professor emeritus, joint appointment, rememberance，新加的內容不用額外的頁面，簡短介紹這些老師就好。名單請參考：https://webpageprodvm.ntu.edu.tw/Journalism/faculty.htm」

**Actions taken:**
- Fetched faculty data from NTU official pages: `adjunct.htm`, `practical-faculty.htm`, `emeritus-professor.htm`, `jointly-appointed-professor.htm`, `remembrance.htm`.
- Added new CSS classes to `css/style.css`: `.faculty-section-heading`, `.heading-fulltime`, `.heading-remembrance`, `.faculty-compact-grid`, `.faculty-compact-card`, `.card-remembrance`, `.faculty-compact-name`, `.faculty-compact-title`, `.faculty-compact-sub`.
- Updated `index.html` Faculty section:
  - Changed "Full-Time Faculty" label from `.faculty-label` to a larger `<h3 class="faculty-section-heading heading-fulltime">`.
  - Added 5 new subsections with compact card grids:
    - **Adjunct Faculty** (3 members): Tai-Li Wang, Shuen-Xiao Chen, Lin-Lin Ku
    - **Adjunct Specialist Faculty** (13 members): Li, Liang, Lee, Lee, Huang, Yang, Liou, Cheng, Shiau, Zhang, Huang, Fang, Wu
    - **Professor Emeritus** (1 member): Chin-Hua Chang
    - **Jointly Appointed Faculty** (2 members): Ching-Yi Liu, Hui-Chieh Su
    - **In Remembrance** (2 members): Rou-Jin Chen, Yen-Yuan Ni

**Files modified:** `css/style.css`, `index.html`

---

## [2026-05-07 ~16:15 TST] — Remove Hero, remove news links, delete first news item

**Prompt summary:**
> 「請幫我 1. 把 HERO 刪掉 2. news 不要有任何的 href 3. news的第一條 2026 entrance刪掉」

**Actions taken:**
- Deleted the `<!-- HERO -->` section (`<div class="hero">`) from `index.html`.
- Changed all 5 `<a class="news-card" href="...">` elements to `<div class="news-card">` (removed all `href`, `target`, `rel` attributes).
- Deleted the first news card "2026 Entrance Examination and Admissions Brochure".
- Synced `index.html` to main repo folder.

**Files modified:** `index.html`

---

## [2026-05-07 ~18:25 TST] — All faculty tabs use full-time card style; remove Chao-Hwei Huang; add Wan-Yu Wu photo

**Prompt summary:**
> 「請幫我把所有 faculty 的 card 改成和 fulltime faculty 一樣，另外幫我把 adjunct 裡面的 Chao-Hwei Huang 整個拿掉，並且要增加 Wan-Yu Wu 的圖片（在 image 資料夾）」

**Actions taken:**
- Converted all 5 non-full-time tab panels (Adjunct, Adjunct Specialist, Professor Emeritus, Jointly Appointed, In Remembrance) from `.faculty-compact-grid` / `.faculty-compact-card` to `.faculty-grid` / `.faculty-card`, matching the full-time faculty card layout (300px photo on top, name/badge/tags below).
- Removed Chao-Hwei Huang (黃兆徽) entirely from the Adjunct Specialist panel.
- Replaced Wan-Yu Wu's character placeholder with `<img src="image/Wan-Yu%20Wu.jpg">`.
- Added `.faculty-card-remembrance` CSS variant (gray top border, slight opacity) for In Remembrance cards.

**Files modified:** `css/style.css`, `index.html`

---

## [2026-05-07 ~18:10 TST] — Faculty section: NHK-style tab switcher

**Prompt summary:**
> 「faculty 那塊我想要改成 nhk網站中 class為section-colored-nowonair的那種感覺，也就是有按鈕可以切換目前看到的內容」

**Actions taken:**
- Added a `.faculty-tab-bar` with 6 `<button class="faculty-tab-btn">` elements (Full-Time, Adjunct, Adjunct Specialist, Prof. Emeritus, Jointly Appointed, In Remembrance).
- Wrapped each faculty category in a `<div class="faculty-tab-panel">` with a matching `id` (`faculty-fulltime`, `faculty-adjunct`, `faculty-specialist`, `faculty-emeritus`, `faculty-joint`, `faculty-remembrance`); only the first panel has `class="active"` by default.
- Added CSS: tab buttons styled with a browser-tab look (rounded top corners, maroon filled when active); panels use `display:none` / `display:block` toggling.
- Added JS: clicking a tab button hides all panels, shows the selected one, and updates `aria-selected`.
- Updated sidebar sub-nav links to use `data-faculty-tab` attributes; added JS handler that activates the matching tab and smooth-scrolls to the faculty section.

**Files modified:** `css/style.css`, `index.html`

---

## [2026-05-07 ~17:50 TST] — Font size, photo height, pillar layout, sidebar sub-nav, remove sidebar header

**Prompt summary:**
> 「1. 整體非標題的文字幫我加大 2. 把 index 介面的 full-time faculty 的照片，高度改為 300 3. introduction 右側的 grid 改為一個 column，不要兩個 4. navigation bar 保留 introduction, news 和 faculty 就好，faculty 下面可以增加 fulltime, adjunct...... 的子欄位 5. navigation bar 上面的「Graduate Institute of Journalism 國立臺灣大學新聞研究所 Cultivating Journalism Talent for a New Era」拿掉」

**Actions taken:**
- `body { font-size: 18px }` (up from 16px).
- `.faculty-photo-wrap { height: 300px }` (up from 200px).
- `.intro-pillars { grid-template-columns: 1fr }` (collapsed from 2-col).
- Removed `.sidebar-institute` block from sidebar HTML.
- Replaced sidebar nav with 3 top-level links (Introduction, News, Faculty); added 6 sub-items under Faculty linking to anchors `#faculty-fulltime`, `#faculty-adjunct`, `#faculty-adjunct-specialist`, `#faculty-emeritus`, `#faculty-joint`, `#faculty-remembrance`.
- Added corresponding `id` attributes to all 6 faculty subsection `<h3>` headings.
- Added `.sidebar-nav-sub-list` and `.sidebar-nav-sub-link` CSS.
- Cleaned up now-redundant responsive `.intro-pillars` overrides.

**Files modified:** `css/style.css`, `index.html`

---

## [2026-05-07 ~17:35 TST] — Left sidebar nav + slim top header (NHK-style layout)

**Prompt summary:**
> 「請幫我把 navigator bar 移至左側，最上面的新聞所 bar 再小一點，感覺會像：https://www.nhk.or.jp/」

**Actions taken:**
- Replaced large `.site-banner` + horizontal `.site-nav` with:
  - `.site-header` — 54px slim sticky top bar (maroon) with site name, Chinese sub-title, and 中文 language link
  - `.site-layout` flex wrapper containing `.site-sidebar` (210px sticky left nav) + `.site-main` (flex content area)
  - `.site-sidebar` — white background, left-border active indicator (gold), institute mini-card on top, then nav links
- Rewrote scroll-spy JS to target `.sidebar-nav-link[data-section]` instead of old `.nav-link`
- Added responsive breakpoints: sidebar narrows to 170px at ≤960px; collapses to horizontal strip at ≤720px
- Updated all 7 `faculty/*.html` to use the new `.site-header` (replacing `.site-banner`)

**Files modified:** `css/style.css`, `index.html`, all 7 `faculty/*.html`

---

## [2026-05-07 ~17:20 TST] — Footer 2/3+1/3 layout; remove nav from faculty pages

**Prompt summary:**
> 「請幫我把 footer 改成左邊是 Graduate Institute of Journalism 的小簡介（內容不改），占寬度的 2/3；右邊是聯絡方式（內容不改），占寬度的 1/3。另外，再幫我把所有 fulltime faculty 的網頁拿掉 navigator」

**Actions taken:**
- Changed `.footer-cols` from `grid-template-columns: 2fr 1fr 1fr` to `2fr 1fr`; updated responsive breakpoint at ≤960px to collapse to `1fr` (was `1fr 1fr`).
- Removed the "Quick Links" `<div class="footer-col">` from `index.html` and all 7 faculty pages.
- Removed `<nav class="site-nav">` from the 5 faculty pages that had the new banner structure.
- For `lih-yun-lin.html` and `i-i-chan.html` (still had old `topbar`+`navbar` structure): replaced with new `<header class="site-banner">` and removed `<nav class="navbar">`, bringing them in line with the other 5 faculty pages.

**Files modified:** `css/style.css`, `index.html`, all 7 `faculty/*.html`

---

## [2026-05-07 ~17:10 TST] — Compact faculty: 3-column grid, larger name & photo

**Prompt summary:**
> 「我覺得除了 fulltime faculty 的老師名字都太小了，請幫我將所有人的名字格式，改成和 fulltime faculty 一樣的大小。同時，將除了 fulltime faculty 以外的其他區塊，從原本的一列兩個 card 變成一列三個 card，且照片再大一點」

**Actions taken:**
- Changed `.faculty-compact-grid` from `repeat(2, 1fr)` to `repeat(3, 1fr)`.
- Added responsive fallback: 2 columns at ≤960px, 1 column at ≤600px.
- Increased `.faculty-compact-name` font-size from `0.95rem` to `1.04rem` (matching `.faculty-name`).
- Enlarged `.faculty-compact-photo-wrap` from 64×76px to 80×96px; bumped placeholder font-size accordingly.

**Files modified:** `css/style.css`

---

## [2026-05-07 ~17:00 TST] — Switch all faculty photos to local image/ folder

**Prompt summary:**
> 「我有將所有 faculty 的照片放在 image 資料夾，請幫我將照片來源更新為 image 資料夾中的照片」

**Actions taken:**
- Copied `image/` folder from main repo into worktree.
- Ran Python batch script to replace all NTU media-server `src="https://webpageprod-ws..."` URLs with local `image/<Name>.<ext>` paths (URL-encoded spaces as `%20`) across `index.html` and all 7 `faculty/*.html` files; also removed `onerror` fallback handlers since files are now local.
- Replaced character placeholder divs for Lih-Yun Lin and I-I Chan (both in `index.html` and their profile pages) with proper `<img>` tags pointing to local files.

**Files modified:** `index.html`, `faculty/lih-yun-lin.html`, `faculty/i-i-chan.html`, `faculty/ji-lung-hsieh.html`, `faculty/chen-ling-hung.html`, `faculty/adrian-rauchfleisch.html`, `faculty/hui-ju-tsai.html`, `faculty/lokman-tsui.html`

---

## [2026-05-07 ~16:45 TST] — Compact faculty grid: 2-column layout, maroon/gray name colors

**Prompt summary:**
> 「請把除了 full-time faculty 以外的所有 faculty，將原本一列四個老師改為一列兩位老師，card 內容改為左邊為圖片，右邊為老師名字、職稱（如果有再加）、授課項目。老師的名字顏色格式如同 full-time faculty，英文名為 #671919，中文部分為灰色」

**Actions taken:**
- Changed `.faculty-compact-grid` from `repeat(auto-fill, minmax(240px, 1fr))` to `repeat(2, 1fr)` so exactly 2 cards appear per row.
- Added `@media (max-width: 600px)` breakpoint to collapse compact grid to 1 column on small screens.
- Name color (`.faculty-compact-name`) was already `var(--maroon)` = `#671919`; Chinese span (`.faculty-compact-zh`) was already `var(--text-500)` = gray — no change needed.

**Files modified:** `css/style.css`

---

## [2026-05-07 ~16:30 TST] — Add photos and Chinese-name styling to all compact faculty cards

**Prompt summary:**
> 「針對所有index.html 的所有 faculty card，我希望格式可以像 full-time faculty 一樣，中文名以灰色小字呈現 另外所有人請附上照片，但放在 card 左邊、小張圖片就好」

**Actions taken:**
- Added horizontal flex layout CSS to `css/style.css`: `.faculty-compact-photo-wrap`, `.faculty-compact-photo`, `.faculty-compact-placeholder-sm`, `.faculty-compact-info`, `.faculty-compact-zh`.
- Fetched photo URLs for all 21 compact faculty members from NTU official pages (`adjunct.htm`, `practical-faculty.htm`, `emeritus-professor.htm`, `jointly-appointed-professor.htm`, `remembrance.htm`).
- Rewrote all 21 compact cards in `index.html` to use the new horizontal layout: photo wrap on the left (64×76px), info block on the right with English name + `<span class="faculty-compact-zh">(中文名)</span>` in gray small text.
- Wan-Yu Wu uses a character placeholder (吳) as her photo URL matched another faculty member's, likely a scraping error.

**Files modified:** `css/style.css`, `index.html`

---

## [2026-05-07 ~17:00 TST] — Convert all non-full-time faculty cards to full-time card style; remove Chao-Hwei Huang; add Wan-Yu Wu photo

**Prompt summary:**
> 「請幫我把所有 faculty 的 card 改成和 fulltime faculty 一樣，另外幫我把 adjunct 裡面的 Chao-Hwei Huang 整個拿掉，並且要增加 Wan-Yu Wu 的圖片（在image資料夾）」

**Actions taken:**
- Replaced all 21 compact cards (`.faculty-compact-grid` / `.faculty-compact-card`) in the 5 non-full-time panels with full-size cards using `.faculty-grid` / `.faculty-card` (300px photo, badge, tags), matching the full-time panel layout.
- Removed Chao-Hwei Huang's card from the Adjunct Specialist panel entirely.
- Added `<img class="faculty-photo" src="image/Wan-Yu%20Wu.jpg">` for Wan-Yu Wu, replacing the character placeholder.

**Files modified:** `index.html`

---

## [2026-05-07 ~17:20 TST] — Full-width footer; suppress non-full-time hover effects; make full-time cards fully clickable

**Prompt summary:**
> 「1. footer 的寬度請幫我撐到網頁寬，不要讓 navigator 區塊壓住它。2. 除了 fulltime faculty 的其他faculty，在滑鼠點到他們的名字時，不要有底線。滑鼠點到他們的 card 時，不要讓 card 浮起來。3. 點選 fulltime faculty 的 card 的任何位置，就可以連到他們各自的網站」

**Actions taken:**
- Moved `<footer>` outside of `<div class="site-layout">` so it renders as a full-width block-level element, no longer constrained by the 210px sidebar column.
- Changed all 7 full-time faculty cards from `<div class="faculty-card">` to `<a class="faculty-card" href="faculty/[name].html">` so the entire card is clickable; replaced inner `<a class="faculty-name">` with `<span class="faculty-name">` to avoid nested anchors.
- Added CSS in `style.css`:
  - `a.faculty-card { display:block; text-decoration:none; color:inherit; cursor:pointer; }` — makes the `<a>` wrapper behave like the old `<div>`.
  - `a.faculty-card:hover .faculty-name { text-decoration: underline; }` — preserves name underline on hover for full-time cards only.
  - `.faculty-tab-panel:not(#faculty-fulltime) .faculty-card:hover { box-shadow:none; transform:none; cursor:default; }` — suppresses card lift and pointer cursor on all non-full-time panels.
  - Removed old `.faculty-name:hover { text-decoration: underline; }` rule that would have applied to non-full-time cards.

**Files modified:** `index.html`, `css/style.css`

---

<!-- Template for future entries:

## [YYYY-MM-DD HH:MM TST] — Short title

**Prompt summary:**
> 「...」

**Actions taken:**
- ...

**Files modified/created:** ...

-->
