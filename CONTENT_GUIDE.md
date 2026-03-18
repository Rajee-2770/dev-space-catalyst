# Dev Hub — Content & UI/UX Guide

A reference for building new topic pages that stay visually consistent with `index.html` and `pages/Arrays&LL.html`.

---

## File Structure

```
ZSGS/
├── index.html                      ← Landing page (quotes + topic picker)
├── CONTENT_GUIDE.md                ← This file
└── pages/
    └── Arrays&LL.html              ← Topic 1: Arrays, ArrayList & LinkedList
    └── <NextTopic>.html            ← Future topics follow this pattern
```

---

## Design System

### Color Palette

| Token | Hex | Usage |
|---|---|---|
| `--dark` | `#0f172a` | Page background, dark slides |
| `--dark2` | `#1e293b` | Card backgrounds, secondary dark |
| `--blue` | `#3b82f6` | Primary accent, Array badge |
| `--green` | `#10b981` | ArrayList badge, success states |
| `--orange` | `#f97316` | Singly LL badge, warning states |
| `--red` | `#ef4444` | Doubly LL badge, danger states |
| `--purple` | `#8b5cf6` | Circular LL badge, answer labels |
| `--amber` | `#f59e0b` | Highlight formulas |
| `--teal` | `#14b8a6` | Eyebrow labels, subtle accents |
| `--gray` | `#64748b` | Body text, subtitles |
| `--border` | `rgba(148,163,184,.15)` | Card and section borders |

### Typography

- **Font family:** `'Segoe UI', system-ui, sans-serif`
- **Headings:** `font-weight: 700–800`
- **Body text:** `font-size: 13–14px`, `line-height: 1.6`
- **Badges/labels:** `font-size: 9–10px`, `font-weight: 700`, `letter-spacing: 0.5–1.5px`

### Slide Theme Classes

Each slide `<div class="slide">` can take one of:

| Class | Gradient | Use for |
|---|---|---|
| *(none)* | White background | Concept / visual slides |
| `.dark` | `#0f172a → #1e293b → #0f3460` | Title slides, Q&A slides |
| `.dark2` | `#064e3b → #0f172a` | ArrayList / green-themed slides |
| `.dark3` | `#4c1d95 → #0f172a` | Circular LL / purple-themed slides |

---

## index.html — Page Anatomy

```
┌─────────────────────────────┐
│  Header (sticky, blurred)   │
│  Logo · "SOFTWARE DEV PATH" │
├─────────────────────────────┤
│  Quote Section              │
│  ─ Eyebrow label            │
│  ─ Random quote (150 pool)  │
│  ─ Author                   │
│  ─ [↻ New Quote] button     │
│  ─ #N of 150 counter        │
├─────────────────────────────┤
│  "Pick a Topic" heading     │
│                             │
│  [Topic Card]  [Card Soon]  │
│  [Card Soon]   …            │
├─────────────────────────────┤
│  Footer                     │
└─────────────────────────────┘
```

### Adding a New Topic Card

Copy this template into `index.html` inside `.topic-grid`:

```html
<a class="topic-card" href="pages/YourTopic.html">
  <div class="card-icon">🔢</div>
  <div class="card-label">DSA · Topic N</div>
  <div class="card-title">Your Topic Title</div>
  <div class="card-desc">Brief description of what students will learn.</div>
  <div class="card-tags">
    <span class="card-tag tag-blue">Subtopic A</span>
    <span class="card-tag tag-green">Subtopic B</span>
  </div>
  <div class="card-footer">
    <span class="card-stat"><b>N</b> Questions · Slides</span>
    <div class="card-arrow">→</div>
  </div>
</a>
```

**Card colour variants** — add class to `.topic-card`:

| Class | Top border | Icon bg | Label |
|---|---|---|---|
| *(default)* | blue→purple | blue tint | blue |
| `.green` | green→teal | green tint | green |
| `.orange` | orange→amber | orange tint | orange |
| `.red` | red→pink | red tint | red |
| `.purple` | purple→blue | purple tint | purple |

**Tag colour variants** for `.card-tag`:
`tag-blue`, `tag-green`, `tag-orange`, `tag-red`, `tag-purple`

---

## Topic HTML Page — Structure Template

Every topic page should follow the `Arrays&LL.html` pattern exactly:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Topic Name — Data Structures</title>
  <style>
    /* ── Copy all CSS from Arrays&LL.html verbatim ── */
    /* Keep: *, :root, body, .deck, .slide, .dark/.dark2/.dark3, */
    /*        .pad, .badge, .tag, h2, .sub, .mem, .node-chain,   */
    /*        .stat-grid, .q-box, .a-box, .q-title, .hint-label, */
    /*        .ans-label, .text-sm, .controls, .btn-*, .dots,    */
    /*        .dot, .counter, .tbl, .formula, .grid-*, .card-sm, */
    /*        .reveal-btn, .hidden, .level, .codebox, .hint-btn, */
    /*        .nav-btn, .nav-left, .nav-right,                    */
    /*        .toolbar, .tb-btn, .tb-home, .tb-print,            */
    /*        @media print { … }                                  */
  </style>
</head>
<body>

<div class="deck" id="deck"></div>

<!-- Floating toolbar — keep on every page -->
<div class="toolbar">
  <button class="tb-btn tb-home" onclick="window.location.href='../index.html'">← Home</button>
  <button class="tb-btn tb-print" onclick="printAllSlides()">⎙ Print PDF</button>
</div>

<script>
const S = [

  // ── SLIDE 0: TITLE (always dark) ──
  {dark:true, html:`
    <div class="pad" style="align-items:center;justify-content:center;text-align:center">
      <div style="font-size:12px;letter-spacing:3px;color:#7ec8e3;margin-bottom:18px">DATA STRUCTURE &nbsp; ALGORITHM</div>
      <h2 style="font-size:36px;color:#f1f5f9;margin-bottom:8px">Your Topic Title</h2>
      <div style="display:flex;gap:10px;justify-content:center;flex-wrap:wrap;margin-top:14px">
        <span style="padding:4px 14px;border-radius:16px;border:1px solid #3b82f6;font-size:11px;color:#3b82f6">Tag A</span>
      </div>
    </div>`},

  // ── SLIDE 1: CONCEPT SLIDE ──
  {html:`
    <div class="pad">
      <span class="badge" style="background:#3b82f6">TOPIC</span>
      <h2>Concept Title</h2>
      <p class="sub">One-line description</p>
      <!-- content -->
    </div>`},

  // ── QUESTION SLIDE TEMPLATE ──
  {dark:true, html:`
    <div class="pad">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <span class="badge" style="background:#3b82f6">TOPIC</span>
        <span class="tag" style="background:#10b98122;color:#10b981">EASY</span>
      </div>
      <div class="q-title" style="margin-top:8px">Q1: Question text here?</div>
      <div class="q-box">
        <div class="hint-label">HINT</div>
        <div class="text-sm">Your hint text.</div>
      </div>
      <div class="a-box">
        <div class="ans-label">
          ANSWER
          <button class="reveal-btn"
            onclick="this.parentElement.nextElementSibling.classList.toggle('hidden');
                     this.textContent=this.textContent==='Reveal'?'Hide':'Reveal'">Reveal</button>
        </div>
        <div class="hidden">
          <div class="text-sm" style="margin-top:6px">Your answer here.</div>
        </div>
      </div>
    </div>`},

];

// ── ENGINE (copy verbatim from Arrays&LL.html) ──
// … (build slides, nav buttons, goTo, go, setupQuestionInteractivity,
//    updateNavButtons, keydown listener, printAllSlides) …
</script>
</body>
</html>
```

---

## Slide Types Cheat Sheet

### Concept Slide (white background)
```js
{html:`
  <div class="pad">
    <span class="badge" style="background:#3b82f6">ARRAY</span>
    <h2>Title</h2>
    <p class="sub">Subtitle</p>
    <!-- memory diagram, code box, grid, table … -->
  </div>`}
```

### Q&A Slide (dark background)
```js
{dark:true, html:`
  <div class="pad">
    <div class="q-title">Q1: Question?</div>
    <div class="q-box">
      <div class="hint-label">HINT</div>
      <div class="text-sm hidden">Hint text</div>
    </div>
    <div class="a-box">
      <div class="ans-label">ANSWER <button class="reveal-btn" ...>Reveal</button></div>
      <div class="hidden"><div class="text-sm">Answer</div></div>
    </div>
  </div>`}
```

### Difficulty Tags
```html
<span class="tag" style="background:#10b98122;color:#10b981">EASY</span>
<span class="tag" style="background:#f9731622;color:#f97316">MEDIUM</span>
<span class="tag" style="background:#ef444422;color:#ef4444">SENIOR</span>
```

### Code Box
```html
<div class="codebox">int arr[5] = {10, 20, 30};</div>
```

### Formula Box
```html
<div class="formula">address = base + (index × size)</div>
```

### Memory Cell Row
```html
<div class="mem">
  <div class="mem-cell" style="background:#eff6ff;border-color:#93c5fd;color:#1d4ed8">10</div>
  <div class="mem-cell" style="background:#f0fdf4;border-color:#6ee7b7;color:#065f46">20</div>
  <div class="mem-empty">—</div>
</div>
```

### Node Chain (LinkedList)
```html
<div class="node-chain">
  <div class="nd" style="background:#eff6ff;border-color:#93c5fd;color:#1d4ed8">
    10<div class="nd-sub">0x100</div>
  </div>
  <div class="arrow-r">→</div>
  <div class="nd" style="...">20</div>
</div>
```

### Comparison Grid
```html
<div class="grid-3">
  <div class="card-sm" style="background:#eff6ff;border:1px solid #bfdbfe">
    <div style="font-size:10px;color:#3b82f6;font-weight:700">ARRAY</div>
    <div class="stat-val">O(1)</div>
    <div class="stat-label">Access</div>
  </div>
</div>
```

---

## Print PDF Feature

Every topic page has a floating **⎙ Print PDF** button (bottom-right).

**How it works:**
1. `printAllSlides()` is called on click.
2. All `.slide` elements get `.active` class → all become visible.
3. `window.print()` triggers the browser's print/PDF dialog.
4. `@media print` CSS ensures: all slides print, one slide per page, nav buttons/toolbar hidden, dark gradients preserve color (`-webkit-print-color-adjust: exact`).
5. After 500 ms, non-current slides are restored to hidden.

**Recommended browser print settings for best PDF:**
- Paper: A4 or Letter
- Orientation: Landscape
- Margins: None or Minimum
- ✅ Background graphics: ON

---

## Motivational Quotes Pool (index.html)

The index page ships with **150 quotes** covering:
- Learning & growth (1–20)
- Coding & programming (21–40)
- Persistence & effort (41–60)
- Problem-solving & DSA (61–80)
- Mindset & confidence (81–100)
- Focus & discipline (101–120)
- Failure & resilience (121–140)
- Purpose & career (141–150)

**To add more quotes**, append to the `QUOTES` array in `index.html`:
```js
{q: "Your quote here.", a: "Author Name"},
```

The counter auto-updates to show `#N of <total>`.

---

## Navigation Flow

```
index.html
  └─[click topic card]──► pages/Arrays&LL.html
                               └─[← Home button]──► index.html
                               └─[⎙ Print PDF]──► browser print dialog
```

---

## Checklist for Each New Topic Page

- [ ] Copy CSS block from `Arrays&LL.html` (including toolbar + print styles)
- [ ] Add floating toolbar with `← Home` and `⎙ Print PDF` buttons
- [ ] Slide 0: dark title slide with topic name and sub-tags
- [ ] Concept slides (3–5) before Q&A slides
- [ ] Q&A slides: each has a hint, a reveal button, a difficulty tag
- [ ] Final slide: summary / comparison table
- [ ] Copy JS engine block verbatim (build loop, `goTo`, `go`, `printAllSlides`)
- [ ] Test keyboard navigation (← →)
- [ ] Test print: all 20 slides render in PDF, colors preserved
- [ ] Add topic card in `index.html` pointing to the new file
- [ ] Update question count on card (`<b>N</b> Questions`)
