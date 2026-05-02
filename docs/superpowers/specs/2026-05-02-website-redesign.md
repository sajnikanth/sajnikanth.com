# Website Redesign Spec
_2026-05-02_

## Goal

Modernise sajnikanth.com: replace the full-page background photo layout with a clean dark card design, add a profile photo, update the tech stack to plain HTML5.

---

## Layout

Single `index.html`, no frameworks, no build step. One centered card on the page.

- Card: max-width 480px, centered horizontally and vertically
- On mobile (≤600px): card goes full-width, no border-radius

---

## Background

- Keep `images/background.jpeg` as the page background
- Apply CSS: `filter: blur(20px) brightness(0.15)`, `background-size: cover`, `background-position: center`, `background-attachment: fixed`
- Remove `images/background_small.jpeg` — no longer needed, CSS handles all screen sizes

---

## Card

- `background: #0f0f0f`
- `border: 1px solid #1e1e1e`
- `border-radius: 12px`
- `padding: 32px`
- Subtle `box-shadow: 0 4px 32px rgba(0,0,0,0.6)`

---

## Card Header

A single flex row:

1. Circular profile photo — 56px × 56px, `border-radius: 50%`, `border: 2px solid #27a9e1`, `object-fit: cover`
   - Source: `images/profile.jpg` (new file — copy from user-provided photo)
2. Name: `Sajnikanth Suriyanarayanan`, 18px, font-weight 600, `#ffffff`
3. Sub-line: `Engineering Manager · Amsterdam`, 12px, `#888888`

Separator below header: 1px horizontal rule, `background: #27a9e1`, `opacity: 0.6`

---

## Card Body

In order:

1. **Bio** — existing text unchanged, 14px, `color: #cccccc`, line-height 1.7
2. **Social icons** — existing 4 icons (email, LinkedIn, Goodreads, GitHub), centered row, 48×48px each, same links as today
3. **Presentations** — section label "Presentations" in 11px uppercase tracking, then 4 existing links in `#27a9e1`, hover → `#ffffff`
4. **Footer** — copyright + year (JS), 11px, `rgba(255,255,255,0.4)`, centered

---

## Typography

- Font: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif
- No external font imports (removes old Google Fonts dependency)

---

## Accent Colour

`#27a9e1` — used for: avatar border, header divider, link colour, hover source

---

## HTML / Tech

- Doctype: `<!DOCTYPE html>` (HTML5, replaces old XHTML transitional)
- Meta charset: `<meta charset="UTF-8">`
- Viewport: `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
- Keep existing Google Analytics snippet (harmless, already in place)

---

## Files Changed

| File | Action |
|---|---|
| `index.html` | Rewrite |
| `images/profile.jpg` | Add (new profile photo) |
| `images/background_small.jpeg` | Delete |

All other files (`background.jpeg`, `email.png`, `linkedin.png`, `goodreads.png`, `github.png`, `favicon.png`) are unchanged.

---

## Out of Scope

- No new pages
- No CMS or templating
- No changes to GA tracking ID
- No changes to existing link URLs
