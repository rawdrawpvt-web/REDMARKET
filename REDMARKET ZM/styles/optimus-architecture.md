# OPTIMUS — Style Architecture (Distilled)

Editorial monochrome. Thin hairline rules. Display serif + mono meta. Almost no color.
Pair with `optimus-tokens.css`. All class names: `op-*`.

---

## 1. DESIGN TOKENS

All in `:root` inside `optimus-tokens.css`. Highlights:

| Group      | Token              | Value                                 |
|------------|--------------------|---------------------------------------|
| color      | `--op-bg`          | `oklch(0.985 0.002 90)` (warm paper)  |
| color      | `--op-fg`          | `oklch(0.120 0.010 60)` (near-black)  |
| color      | `--op-muted-fg`    | `oklch(0.450 0.020 60)`               |
| color      | `--op-live`        | `oklch(0.72 0.18 145)` (ONLY accent — status dots only) |
| color      | `--op-fg-10..70`   | rgba hairline scales                  |
| font       | `--op-font-display`| `'Instrument Serif'`, Georgia, serif  |
| font       | `--op-font-sans`   | `'Instrument Sans'`, system-ui        |
| font       | `--op-font-mono`   | `'JetBrains Mono'`                    |
| type       | `--op-text-hero`   | `clamp(3rem, 12vw, 10rem)`            |
| track      | `--op-track-tight` | `-0.025em`                            |
| track      | `--op-track-widest`| `0.2em` (mono eyebrows)               |
| radius     | `--op-r-md`        | `0.25rem` (base — deliberately tiny)  |
| radius     | `--op-r-full`      | `9999px` (CTAs only)                  |
| shadow     | `--op-shadow`      | `0 4px 12px rgba(0,0,0,0.06)` (nav only) |
| spacing    | 4-pt scale         | `--op-s-1` .. `--op-s-40`             |
| container  | `--op-container-max` | `1400px`                            |
| section    | `--op-section-py`  | `6rem` / `8rem` at lg                 |
| motion     | `--op-ease-smooth` | `cubic-bezier(0.22, 1, 0.36, 1)`      |
| motion     | `--op-ease-spring` | `cubic-bezier(0.34, 1.56, 0.64, 1)`   |
| motion     | `--op-dur-*`       | 200 / 300 / 500 / 700 / 1000ms        |
| breakpoints| sm/md/lg/xl        | 640 / 768 / 1024 / 1280               |

---

## 2. LAYOUT PATTERNS

### `op-container` — page gutter
```html
<div class="op-container"><!-- max 1400, px 24→48 --></div>
```

### `op-section` — vertical rhythm (opt. `--ruled`, `--invert`, `--lg`)
```html
<section class="op-section op-section--ruled">...</section>
<section class="op-section op-section--invert op-section--lg">...</section>
```

### `op-split` — hero / two-up (text + visual, sticky-capable)
```html
<div class="op-split">
  <div><!-- copy --></div>
  <div class="op-sticky-col"><!-- visual or code panel --></div>
</div>
```

### `op-grid-rule` — hairline-gap grid (pricing, metrics)
```html
<div class="op-grid-rule" style="grid-template-columns:repeat(3,1fr)">
  <div class="op-plan">…</div><div class="op-plan op-plan--featured">…</div><div class="op-plan">…</div>
</div>
```

### `op-grid-2 / -3 / -4` — plain responsive grids
```html
<div class="op-grid-3"><div>…</div><div>…</div><div>…</div></div>
```

### `op-grid-overlay` — faint 8×12 grid behind hero
```html
<section class="op-section" style="position:relative">
  <div class="op-grid-overlay"></div>
  <!-- content -->
</section>
```

### `op-noise` — subtle 3% SVG grain on the page root
```html
<main class="op-noise">…</main>
```

### Sticky nav shell (requires JS to toggle `.is-scrolled` after `scrollY > 20`)
```html
<header class="op-nav">
  <nav class="op-nav__inner"><a class="op-nav__brand">…</a><div class="op-nav__links">…</div></nav>
</header>
```

---

## 3. COMPONENT STYLES

| Component       | Class                           | Notes                                           |
|-----------------|---------------------------------|-------------------------------------------------|
| Eyebrow label   | `op-eyebrow`                    | mono + leading 2rem rule. Signature pattern.    |
| Heading         | `op-h1` … `op-h4` / `op-display`| serif, `track-tight`, `lh-tight`                |
| Lead paragraph  | `op-lead`                       | xl, muted, 36rem max                            |
| Caption / meta  | `op-caption`                    | mono, widest track, uppercase                   |
| Outline head    | `op-text-stroke`                | `-webkit-text-stroke` only                      |
| Link underline  | `op-link op-link--underline`    | width-growing underline on hover                |
| Button primary  | `op-btn op-btn--primary`        | fg bg, bg text, full radius                     |
| Button outline  | `op-btn op-btn--outline`        | 1px fg/20 border, fg/5 hover                    |
| Button ghost    | `op-btn op-btn--ghost`          | link-like                                       |
| Button lg / sm  | `op-btn--lg` / `op-btn--sm`     | 56px / 32px heights                             |
| Card            | `op-card` / `--padded`          | 1px fg/10 border, fg/30 + fg/3 on hover         |
| Pricing plan    | `op-plan` / `op-plan--featured` | featured = 2px fg border + negative margin      |
| Plan badge      | `op-plan__badge`                | absolute, fg on bg, mono uppercase              |
| Badge           | `op-badge`                      | mono, rounded-full, fg on bg                    |
| Form input      | `op-input` + `op-label`         | transparent, 1px border, focus = fg border      |
| Toggle          | `op-toggle` `[data-on="true"]`  | rail + knob                                     |
| Code window     | `op-code` + `__chrome/__tabs/__body/__status` | editor chrome + tab underline indicator |
| Live dot        | `op-live-dot`                   | only green usage on entire site                 |
| Metric          | `op-metric__value/__label`      | display 96px, muted label                       |
| Testimonial     | `op-quote` + `op-avatar`        | 60px serif pull-quote                           |
| Marquee row     | `op-marquee` / `--reverse`      | duplicate contents 2× for seamless loop         |
| Integration tile| `op-tile` + `op-tile__title`    | border-reveal + 4px x-shift on hover            |
| Pagination dots | `op-dots` + `op-dots__dot`      | active dot stretches to 2rem wide               |
| Framed CTA      | `op-frame`                      | 1px fg border + decorative corner brackets      |

Minimal markup for the two unique ones:

```html
<!-- Code window -->
<div class="op-code">
  <div class="op-code__chrome">
    <div class="op-code__dots"><span></span><span></span><span></span></div>
    <span class="op-caption">workflow.ts</span>
  </div>
  <div class="op-code__tabs" role="tablist">
    <button class="op-code__tab" aria-selected="true">Install</button>
    <button class="op-code__tab">Initialize</button>
  </div>
  <pre class="op-code__body">…</pre>
  <div class="op-code__status"><span class="op-live-dot"></span>Ready</div>
</div>

<!-- Framed CTA -->
<div class="op-frame">
  <h2 class="op-h2">Ready to build<br>something great?</h2>
</div>
```

---

## 4. ANIMATIONS & TRANSITIONS

| Name              | Class / selector               | Trigger              | Duration / easing                        |
|-------------------|--------------------------------|----------------------|------------------------------------------|
| Char blur-in      | `.op-char-in`                  | mount                | 500ms / `--op-ease-smooth`. Stagger `animation-delay: i * 50ms`. |
| Line reveal       | `.op-line-reveal`              | mount                | 800ms / `--op-ease-expo` (`clip-path`)   |
| Hover lift        | `.op-hover-lift`               | hover                | 500ms / `--op-ease-spring` (translateY -4px) |
| Letter 3D spin    | `.op-letter-spin`              | hover (brand mark)   | 600ms / `--op-ease-spring` (rotateY 360) |
| Scroll reveal     | `.op-reveal` + `.is-visible`   | IntersectionObserver (threshold 0.1–0.2) | 700ms / smooth. Stagger via `style="--op-i: n"`. **JS required.** |
| Marquee L→R       | `.op-marquee`                  | infinite             | 30s linear (translateX 0 → -50%)         |
| Marquee R→L       | `.op-marquee--reverse`         | infinite             | 25s linear (translateX -50% → 0)         |
| Progress fill     | `.op-progress__fill`           | mount                | 5s linear                                |
| Pulse (live dot)  | `.op-live-dot`                 | infinite             | 2s smooth (opacity + scale)              |
| Nav morph         | `.op-nav.is-scrolled`          | `scrollY > 20`       | 500ms smooth. **JS required.**           |
| Mobile menu       | toggle class on `op-nav`       | button click         | stagger links w/ `transition-delay: i*75ms`. **JS required.** |
| Code typewriter   | `.op-code__body` char spans    | tab change / mount   | line 400ms (translate-x) + char 300ms (blur). Stagger `line*80 + char*15 ms`. **JS required** to split chars. |
| Counter           | `op-metric__value`             | IntersectionObserver | 2s custom easeOutCubic (`1 - (1-t)^3`). **JS required.** |

---

## 5. TYPOGRAPHY SYSTEM

| Level             | Font             | Size                                   | Weight | LH   | Track   | Color       |
|-------------------|------------------|----------------------------------------|--------|------|---------|-------------|
| Hero (H1)         | Instrument Serif | `clamp(3rem, 12vw, 10rem)`             | 400    | 0.9  | -0.025em| fg          |
| Section (H2)      | Instrument Serif | 36→60→72px (md/lg)                     | 400    | 0.9  | -0.025em| fg          |
| Sub (H3)          | Instrument Serif | 30→36→48px                             | 400    | 1.1  | -0.025em| fg          |
| Card title (H4)   | Instrument Serif | 24→30px                                | 400    | 1.1  | 0       | fg          |
| Lead              | Instrument Sans  | 20px (lg 24px)                         | 400    | 1.75 | 0       | muted-fg    |
| Body              | Instrument Sans  | 16px                                   | 400    | 1.5  | 0       | fg          |
| Small / meta      | Instrument Sans  | 14px                                   | 400/500| 1.5  | 0       | fg-70       |
| Eyebrow / caption | JetBrains Mono   | 12–14px                                | 400    | 1.5  | 0.2em   | muted-fg    |
| Code              | JetBrains Mono   | 14px                                   | 400    | 1.75 | 0       | fg-70 / -80 |

Rules: headlines are ALWAYS serif + tight tracking. Mono is ONLY for eyebrows, captions, code, status. Sans everywhere else. Never bold > 500.

---

## 6. RESPONSIVE BEHAVIOR

| Breakpoint | What changes                                                                                          |
|------------|-------------------------------------------------------------------------------------------------------|
| base (`<768`) | 1-col grids; section `py: 6rem`; nav links hidden → mobile menu; split hero stacks; sticky col disables; hero marquee stat font 40px |
| `≥768 md`  | grids become 2/3 col; nav links visible; pricing 3-col with hairline gaps; integration tiles inline    |
| `≥1024 lg` | section `py: 8rem`; split hero becomes `1.1fr 0.9fr`; sticky right column engages; H1 up to 10rem; metrics value 6rem; nav inner 3rem horizontal padding |
| `≥1280 xl` | container breathes (stays 1400 max); no structural changes                                            |

Hides at `<768`: `.op-nav__links`, `.op-sticky-col` (becomes relative), lg-only visuals (spheres, tetrahedron).

---

## 7. EDGE CASES & DETAILS

- **Scrollbar:** 10px rail, transparent track, `fg-10` thumb → `fg-30` hover. WebKit-only.
- **Selection:** inverts — `background: fg; color: bg`.
- **Focus ring:** `:focus-visible` → 2px fg outline, 2px offset, 2px radius. Never use `outline: none` without replacement.
- **Placeholders:** `muted-fg`.
- **Overflow:** page root = `overflow-x: hidden` (needed for marquees + oversized hero visuals bleeding right).
- **Backdrop blur:** only on scrolled nav. `color-mix(in oklab, bg 80%, transparent)` + `backdrop-filter: blur(20px)`. Include `-webkit-backdrop-filter`.
- **Mouse spotlight:** CTA frame tracks mouse → radial-gradient at `(x%, y%)`. **JS required**, update inline style on `mousemove`.
- **Invert mode:** `.op-section--invert` flips bg/fg. Re-declare `.op-muted` color override inside (done in tokens file). Hairlines switch to `rgba(255,255,255,0.1)`.
- **Grid-gap as border trick:** `.op-grid-rule` uses `gap:1px; background:fg-10;` and child `background:bg;` → perfect single-pixel dividers at any count without extra borders.
- **Marquee seamlessness:** always render the inner contents TWICE (`[...arr, ...arr]`) inside `.op-marquee`; half-translate = no jump.
- **Counter eased:** `1 - Math.pow(1 - t, 3)` (easeOutCubic) over 2s in `requestAnimationFrame`. **JS required.**
- **Reduced motion:** global override collapses animation/transition durations to `0.01ms` (token file does this).
- **Hatch pattern:** `repeating-linear-gradient(-45deg, transparent 0 40px, currentColor 40px 41px)` at `opacity: 0.03` inside invert sections.
- **Sketch border trick:** `background: linear-gradient(bg,bg) padding-box, linear-gradient(135deg, fg 25%, transparent 25% 50%, fg 50% 75%, transparent 75%) border-box` with 8px tile (rarely used).
- **CTA corner brackets:** `::before`/`::after` on `.op-frame` — 128px boxes with two sides zeroed, `fg-10` border.

**JS needed for these effects (flagged `/* JS */` elsewhere):** sticky-nav morph, scroll reveal (IntersectionObserver), typewriter char split, animated counters, mouse spotlight, word rotator, tab selection state on code window, testimonial carousel, toggle state.
