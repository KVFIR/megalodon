# Design System Master File

> **LOGIC:** When building a specific page, first check `design-system/odin-construction/pages/[page-name].md`.
> If that file exists, its rules **override** this Master file.
> If not, strictly follow the rules below.

---

**Project:** Odin Construction
**Generated:** 2026-07-02 (adapted for dark theme)
**Category:** B2B Service — Construction & Engineering

> Generated via `ui-ux-pro-max` skill (`--design-system`) using query
> `"construction engineering b2b service trust lead generation"`.
> Pattern match: **Trust & Authority** + **Lead Magnet + Form**.
> Typography match confirmed independently: **Lexend / Source Sans 3** ("Corporate Trust" pairing).
>
> The tool's default color recommendation is **light-mode**. This project intentionally uses a
> dark "industrial-luxury" theme (established in the initial site brief), so colors below are
> adapted dark-mode equivalents that preserve the same role mapping and WCAG contrast targets.

---

## Global Rules

### Color Palette (dark theme — actual production tokens)

| Role | Hex | CSS Variable | Contrast vs bg |
|------|-----|--------------|-----------------|
| Background | `#111111` | `--bg` | — |
| Surface | `#171717` | `--surface` | — |
| Surface 2 (inputs) | `#1f1f1f` | `--surface-2` | — |
| Text (primary) | `#f2f0eb` | `--text` | ~15.8:1 |
| Muted (secondary text) | `#b6b1a8` | `--muted` | ~8.9:1 |
| Accent / CTA | `#4d9ad3` | `--accent` | ~6.2:1 (on bg, as button fill w/ dark text) |
| Accent (hover) | `#76b8e8` | `--accent-strong` | higher contrast |
| Border | `#2b2b2b` | `--border` | — |
| Success | `#5baa6c` | `--success` | — |
| Error / Destructive | `#d06b6b` | `--error` | — |

**Color Notes:** Industrial dark neutral + single trust-blue accent, reserved for CTAs and
active/focus states only (matches "Trust & Authority" guidance: one accent color, no gradients,
no playful palettes).

### Typography

- **Heading Font:** Lexend (weights 400/500/600/700)
- **Body Font:** Source Sans 3 (weights 400/500/600/700)
- **Mood:** corporate, trustworthy, accessible, readable, professional, clean
- **Google Fonts:** [Lexend + Source Sans 3](https://fonts.googleapis.com/css2?family=Lexend:wght@400;500;600;700&family=Source+Sans+3:wght@400;500;600;700&display=swap)

**CSS Import (as used in `index.html`):**
```css
--font-heading: 'Lexend', 'Helvetica Neue', Helvetica, Arial, sans-serif;
--font-body: 'Source Sans 3', 'Helvetica Neue', Helvetica, Arial, sans-serif;
```

Applied to: `h1–h6`, `button`, `.btn`, `.logo-wordmark`, `.nav-cta`, `.trust-item strong`,
`.footer-badge-num`. Body copy (paragraphs, labels, form fields) uses `--font-body`.

### Spacing Variables (already in production as 4/8px rhythm)

| Token | Value | Usage |
|-------|-------|-------|
| `--space-2` | `8px` | Icon gaps, inline spacing |
| `--space-3` | `12px` | Tight padding |
| `--space-4` | `16px` | Standard padding |
| `--space-5` | `24px` | Section padding |
| `--space-6` | `32px` | Large gaps |
| `--space-7` | `48px` | Section margins |
| `--space-8` | `64px` | Hero padding |

### Radii

| Token | Value |
|-------|-------|
| `--radius-sm` | `8px` |
| `--radius-md` | `14px` |

---

## Component Specs (as implemented)

### Buttons

```css
.btn-primary {
  background: var(--accent);
  color: var(--bg);
  border: 1px solid var(--accent);
  padding: 12px 24px;
  font-weight: 500;
  min-height: 44px;
  transition: background 150ms ease, border-color 150ms ease, transform 150ms ease;
  cursor: pointer;
}

.btn-primary:hover {
  background: var(--accent-strong);
  border-color: var(--accent-strong);
  transform: translateY(-1px);
}

.btn:active { transform: translateY(0); }
```

### Project Cards

```css
.project-cover img {
  transition: transform 0.3s ease;
}
.project-cover:hover img { transform: scale(1.03); }
```

### Inputs

```css
.form-field input,
.form-field textarea {
  background: var(--surface-2);
  border: 1px solid var(--border);
  padding: 12px 16px;
  border-radius: var(--radius-sm);
  transition: border-color 150ms ease;
}

.form-field input:focus,
.form-field textarea:focus {
  border-color: var(--accent);
}
```

### Modal Gallery

```css
.modal-overlay {
  background: rgba(0, 0, 0, 0.92);
}
```

---

## Style Guidelines

**Style:** Trust & Authority (adapted dark)

**Keywords:** Real project proof (not badges/certs we don't have), trust strip with concrete
metrics, low-friction contact form, direct CTAs.

**Key Effects (applied, motion-safe):**
- Count-up animation on trust-strip / footer numeric stats, gated by `IntersectionObserver`
  and skipped entirely when `prefers-reduced-motion: reduce`.
- Subtle `translateY(-1px)` on button hover (layout-neutral, no reflow).
- `scale(1.03)` image zoom on project cover hover.

### Page Pattern

**Pattern Name:** Hero → Trust strip → Services → Projects → Why us → Contact (see full IA
rationale in the project's PR history — this order was chosen deliberately over the tool's
generic "Lead Magnet + Form" default, because construction/engineering buyers need proof of
delivered work before submitting a quote request.)

---

## Anti-Patterns (Do NOT Use)

- ❌ Fabricated license numbers, certifications, or client logos not confirmed by the business
  (mark as **unspecified** instead of inventing placeholders)
- ❌ Emojis as icons — inline SVG only
- ❌ Missing `cursor: pointer` on clickable elements
- ❌ Layout-shifting hovers — only opacity/color/elevation/translate transforms
- ❌ Text contrast below 4.5:1 (body) / 3:1 (large text, UI glyphs)
- ❌ Instant state changes — use 150–300ms transitions
- ❌ Invisible focus states — `:focus-visible` must always be visible
- ❌ Auto-rotating carousels — galleries are manual, user-controlled (WAI Carousel Pattern)

---

## Pre-Delivery Checklist

- [x] No emojis used as icons (inline SVG only)
- [x] `cursor: pointer` on all clickable elements
- [x] Hover states with smooth transitions (150–300ms)
- [x] Dark mode text contrast ≥ 4.5:1 (verified: text 15.8:1, muted 8.9:1)
- [x] Focus states visible for keyboard navigation (`:focus-visible` outline)
- [x] `prefers-reduced-motion` respected (global transition kill + counter animation guard)
- [x] Responsive: 375px, 768px, 960px, 1200px+ breakpoints covered
- [x] No content hidden behind fixed/sticky nav (sticky nav height accounted for via scroll anchors)
- [x] Skip-to-content link for keyboard users
- [x] Form errors announced via `role="alert"` / `aria-live="assertive"`
