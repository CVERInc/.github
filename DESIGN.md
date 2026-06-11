# CVER design conventions

Shared visual conventions for `CVERInc` products. Adopted 2026-06-11.

## Corner shape — the squircle standard

Every CVER surface with a finite corner radius — cards, buttons, panels,
frames, containers — uses a **continuous-curvature corner (a squircle)**, not
a plain circular arc. The squircle is the Apple-platform corner; we carry the
same shape across the portfolio. Pills and circles stay round (see below).

This is a **progressive enhancement, not a redesign**: existing radii are kept
verbatim, the squircle is layered on top, and anything that can't render it
falls back to the radius you already have. Zero visual regression is a hard
requirement — never trade a working rounded corner for a broken squircle.

The reference implementations are `cver.net` (`src/styles/global.css`,
`--corner`) and `liquidframe` (`liquidframe.css`, `--lf-corner`). Mirror them.

### Web (any CSS)

Add real continuous-curvature corners *on top of* the existing
`border-radius`. Never remove or change a radius to do this.

```css
:root { --corner: squircle; }            /* token, so any layer can override */
.card { corner-shape: var(--corner); }   /* next to its existing border-radius */
```

- `corner-shape: squircle` is `superellipse(2)`. The `border-radius` still
  sizes the corner **and** is the graceful fallback.
- `corner-shape` is **Chromium-only as of mid-2026** — Safari/WebKit and
  Firefox ignore it and keep the `border-radius` arc. That is the whole point:
  pure progressive enhancement, zero regression. Always leave an honest comment
  to that effect next to the rule.
- `corner-shape` **requires a non-zero `border-radius`** to do anything, and is
  **not inherited** — but a custom property *is*. So define the token once on
  `:root` and reference `var(--corner)` everywhere.

**Tailwind projects** — add ONE low-specificity rule to the global/main
stylesheet, covering whichever `rounded-*` utilities the project actually uses.
**Exclude `rounded-full`** — a squircled pill reads wrong.

```css
:root { --corner: squircle; }
:where(.rounded, .rounded-md, .rounded-lg, .rounded-xl, .rounded-2xl, .rounded-3xl) {
  corner-shape: var(--corner);
}
```

**Plain CSS / Svelte / HTML** — put `:root { --corner: squircle; }` in the main
stylesheet, then add `corner-shape: var(--corner);` next to each **finite**
`border-radius` rule on card/button/panel/container surfaces. **Never** on pills
(`border-radius: 9999px` / `99px`) or circles (`border-radius: 50%`) — those
stay round.

### SwiftUI (Swift apps)

Use the **continuous** corner style — the real Apple squircle, fully supported
on Apple platforms (here it actually renders, unlike the web fallback case).

```swift
RoundedRectangle(cornerRadius: x)              // ->  RoundedRectangle(cornerRadius: x, style: .continuous)
.cornerRadius(x)                               // ->  .clipShape(RoundedRectangle(cornerRadius: x, style: .continuous))
.clipShape(RoundedRectangle(cornerRadius: x))  // ->  add `, style: .continuous`
```

Leave `Capsule()`, `Circle()`, and capsule-style pills unchanged.

### When this does not apply

Skip the standard, don't invent UI to satisfy it: bots with no UI, docs-only
repos, Apps-Script/Sheets backends with no styled HTML, and repos whose only
radius is pills/circles. A clean skip is correct, not a gap.
