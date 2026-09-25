---
name: slide-figure
description: Use when the user needs a figure, diagram, or chart designed for a slide or presentation — something that reads clearly when projected. Produces a single, self-contained figure (SVG or PNG) with slide-appropriate sizing, contrast, and minimal labeling. Triggers on "figure for my slide", "diagram for the deck", "chart for the presentation", "make this readable on a projector".
---

# Slide Figure

Create a single figure meant to be dropped onto a presentation slide. The goal is legibility from the back of a room, not density — a slide figure carries one idea.

## Principles

- **One idea per figure.** If the content needs two ideas, make two figures.
- **Big enough to read projected.** Minimum ~24px equivalent for body labels, ~32px+ for titles, at the figure's intended display size.
- **High contrast.** Dark ink on light ground (or the reverse); avoid thin gray hairlines that vanish on a projector.
- **Minimal chrome.** Drop gridlines, legends, and axis ticks that don't earn their place. Label series directly where possible.
- **Safe margins.** Keep content inside a margin so nothing clips against slide edges.

## Output

- Default to **SVG** (scales cleanly, editable). Offer PNG at 2x when a raster is needed.
- Target a **16:9** frame unless told otherwise; common working size 1280×720.
- Deliver a single self-contained file with fonts as system-safe stacks (e.g. `-apple-system, Segoe UI, Roboto, sans-serif`).

## Workflow

1. Ask (or infer) the **one idea** the figure must convey and the **display context** (light or dark deck, aspect ratio).
2. Pick the simplest form that carries it: a labeled diagram, a single-series chart, a flow, or a comparison.
3. Draw it with generous type, direct labels, and a restrained palette (1 accent color + neutrals).
4. Save to the path the user wants and send the file so they can preview it.

## Palette

Use a neutral base with a single accent:

- Ink: `#1a1a1a`
- Ground: `#ffffff`
- Muted: `#6b7280`
- Accent: `#2563eb` (swap for the deck's brand color when known)

For a dark deck, invert ink/ground and lift the accent's lightness.
