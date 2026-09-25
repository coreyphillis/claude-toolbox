---
name: slide-figure
description: Converts a publication-style R figure (ggplot2 or base R) into a presentation-ready version for Corey's slide template. Use when Corey asks to turn a figure into a slide/presentation version, make a figure "deck-ready," recreate a plot for a talk, or produce a light/dark version of an existing figure for a presentation.
---

# Publication figure → slide figure

Corey's figures start as publication graphics: dense, small-font, built for a
reader who can sit with them up close. This skill produces a presentation
version for a large, well-lit (or dark) room, matching his slide deck's theme.

**Reuse the same data-prep/analysis code as the publication figure.** Branch
only at the plotting/theme layer, so the publication and slide versions never
drift apart in the underlying data.

## Ask before generating, if not already specified

1. **Theme** — light-room or dark-room version (or both)?
2. **Target size** — full one-idea slide (~8.5 × 4.4 in) or a half-slide
   comparison card (~5.0 × 4.0 in), or a custom size?

Don't guess these — ask.

## Typography

- Font: Calibri. Verify availability with `systemfonts::system_fonts()`
  first; fall back to Arial/Helvetica if unavailable. Do **not** use
  `extrafont::font_import()` or `showtext::font_add_google()` — both can hit
  GitHub/internet blocks on Corey's corporate network.
- Sizes, at final render size (never scale up/down after export):
  - Axis titles: 18–20pt
  - Axis tick labels: 16pt
  - Direct data/line-end labels: 16–18pt (bold for the one number that matters)
  - No plot title/subtitle/caption in the figure itself — the slide title
    carries the takeaway.
- Line width 1.5–2× the publication version; point size increased to match.

## Color — always override defaults with these exact values

Never use ggplot2 or base R default palettes.

| Role | Light theme | Dark theme |
|---|---|---|
| Primary (water) | `#205072` | `#8FC1DE` |
| Secondary (earth) | `#B98243` | `#E3B36A` |
| Tertiary (moss) | `#5B7B6F` | `#8FB09F` |
| Accent (clay) | `#A85C32` | `#E08F5F` |
| Text | `#1E2B2E` | `#F3EFE6` |
| Background | `#FFFFFF` | `#13262B` |
| Gridline/caption | `#6E6A61` | `#AFB6AE` |

Map series in this order: water → earth → moss → clay. If a figure needs more
than 4 series, don't add more colors — flag it to Corey; it likely means the
figure should be split or faceted across multiple slides instead.

## Simplification (presentation Tufte, not publication Tufte)

- Drop minor gridlines entirely; major gridlines only if the audience needs
  to read an exact value, otherwise none.
- No panel border/box.
- Replace the legend with direct labels at the line/bar end when ≤4 series;
  delete the legend.
- Cut any facet/panel not essential to *this slide's* one idea — split
  across slides rather than shrinking multiple panels to fit.
- No 3D, shadows, or decorative chart junk.

## Background handling

Match the target theme's background exactly (`panel.background` /
`plot.background` in ggplot2; device background in base R). Only leave it
transparent if Corey says the figure is going onto a colored card rather than
the plain slide background.

## Export

Always produce both formats:

- **PNG**, 300 dpi, via `ragg::agg_png()` (ggplot2) or `png(type="cairo")`
  (base R) for clean anti-aliasing.
- **SVG**, via `ggsave(..., device = "svg")` (needs `svglite`, CRAN-only) or
  base R's built-in `svg()` device. Neither requires a GitHub install.

Dimensions match the placeholder from the questions above. Filename
convention: `<topic>_<theme>.png` / `.svg`, e.g. `cooling_days_light.svg`,
`cooling_days_dark.svg`.

After rendering, check for label collisions — spacing that worked at 8pt in
the publication version often overlaps at 16–20pt. Fix by adjusting margins
or expansion factors; don't shrink the font back down to make it fit.
