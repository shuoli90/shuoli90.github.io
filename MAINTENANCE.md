# Site Maintenance Guide

A short reference for updating `shuoli90.github.io`.

## Where things live

| File / dir | What's in it |
|---|---|
| `index.html` | All content: name, about, experience, publications, contact, footer |
| `css/style.css` | Visual style: colors, typography, layout |
| `materials/papers/*.pdf` | Local copies of your papers (linked from publications) |
| `materials/cv/Resume_Shuo_Li.pdf` | CV linked from the header |
| `images/` | Profile photo (`personal.png`), featured-paper thumbnails (`MoCAN.png`, `rank.png`, `traq.png`), icons |

---

## Common updates — exact recipes

### 1. Add a new publication

In `index.html`, find the right year section inside `<section id="publications">`, and insert a new `<li>` block in the matching `<ul class="pub-list">`:

```html
<li>
    <span class="pub-num">[NN]</span>
    <span class="pub-title">Title of the paper</span>
    <span class="pub-meta">
        <span class="venue">Venue YYYY</span>
        <span class="pub-links">
            <a href="https://arxiv.org/abs/XXXX.XXXXX" target="_blank" rel="noopener">arXiv</a>
            <a href="materials/papers/YOUR_FILE.pdf" target="_blank" rel="noopener">PDF</a>
        </span>
    </span>
</li>
```

If the PDF lives locally, drop it into `materials/papers/` first.

### 2. Add or edit an experience entry

In `index.html`, inside `<section id="experience">`, copy an existing `<div class="experience">` block and edit dates, role, org, and bullets. Bullet color follows position — the first experience gets red triangles, the second gets blue. To add a colour for a third role, add this to `style.css`:

```css
.experience:nth-of-type(3) ul li::before { color: var(--c-green); }
```

### 3. Update About text or research interests

Same file, sections `#about` (paragraphs) and `#research` (the `<ul class="tag-list">`).

### 4. Swap the profile photo

Replace `images/personal.png`. Keep roughly portrait aspect ratio (the box is 150×190). The red offset block + yellow corner block are pure CSS — no markup edits needed.

### 5. Update the CV

Drop the new PDF over `materials/cv/Resume_Shuo_Li.pdf` (same filename = no markup changes).

### 6. Change external links

In `index.html` header, find the `<p class="header-links">` block. Five links: Email, Google Scholar, LinkedIn, GitHub, CV.

### 7. Add a new featured publication card

Under `<section id="publications">`, after the "Featured" heading, copy an existing `<div class="publication">` block. To give it a new venue-badge colour, add to CSS:

```css
.publication:nth-of-type(4) .venue-badge { background: var(--c-yellow); color: var(--ink); }
```

---

## Colour palette

Defined at the top of `css/style.css`. Change any value once and every consuming element updates.

| Variable | Hex | Used for |
|---|---|---|
| `--c-red` | `#d33b3b` | "01 About", Vol.02 chip, photo offset block, first experience bullets, Featured year bar, first venue badge |
| `--c-blue` | `#1d4ed8` | "02 Research", second experience bullets, 2026 year bar, default venue badges |
| `--c-yellow` | `#e0a82e` | "03 Experience", small corner block on photo, 2024 year bar |
| `--c-green` | `#15803d` | "04 Publications", 2025 year bar, second featured venue badge |
| `--c-magenta` | `#be185d` | "05 Contact", 2023 year bar, third featured venue badge |
| `--c-cobalt` | `#1e40af` | "Earlier" year bar |
| `--ink` | `#0a0a0a` | Body text, rules, borders |
| `--bg` | `#f4f2eb` | Page background (warm off-white) |

---

## Git snapshots (rollback points)

```bash
git log --oneline
```

Design snapshots in this repo's history:

| Hash | Look |
|---|---|
| latest | Brutalist Swiss + colorful (current) |
| `46aa224` | Glassmorphic dark + steel-blue |
| `201b1ed` | Terminal aesthetic + boot animation |
| `9e396ea` | Clean modern light layout |
| `217ae5d` | Original site |

Roll back to any version without losing committed history:

```bash
git checkout <hash> -- index.html css/style.css
```

---

## Local preview

```bash
open index.html
```

No build step — plain HTML/CSS. Reload the browser after edits.

---

## Deploying

This repo is a GitHub Pages user site. Commit and push to `master`:

```bash
git add -A
git commit -m "your message"
git push origin master
```

Live at `https://shuoli90.github.io` within a minute or two.
