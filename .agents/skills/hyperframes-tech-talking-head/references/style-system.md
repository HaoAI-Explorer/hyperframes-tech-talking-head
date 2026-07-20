# Style System

Use this reference when selecting typography, colors, screenshot treatment, layout, motion intensity, and audio restraint.

## Visual Identity

Use a restrained multi-accent palette:

| Role | Default | Use |
|---|---|---|
| Graphite | `#0B1014` | Full-frame base and deep panels |
| Cool white | `#F5F7FA` | Primary Chinese copy |
| Muted white | `#AEB8C4` | Metadata and secondary notes |
| Electric blue | `#5AA3FF` | Codex, code, active states |
| Cyan | `#35D0BA` | HyperFrames, connections, passes |
| Acid yellow | `#E3FF52` | One decisive word or warning only |

Do not let one hue dominate the whole video. Avoid large blue gradients, neon-purple templates, beige editorial themes, glowing particle fields, and decorative HUD frames.

## Typography

- Use a bold Chinese sans-serif for claims and a mono face such as JetBrains Mono for technical metadata.
- Main claim: normally `72-108px` on a `1080x1920` canvas.
- Screenshot explanation: `44-58px`; do not rely on captured desktop UI text as the primary message.
- Compact metadata: `24-34px`, high contrast, short lines.
- Keep letter spacing at `0`; never use viewport-scaled font sizing.
- Keep titles to one or two short lines. Rewrite rather than shrinking below phone-readable size.

## Mobile Layout

- Reserve the detected burned-subtitle band as a hard safe zone. Until measured, treat the lower `18%` of the canvas as protected.
- Face visibility is optional. Cover it only when the takeover proves or explains the spoken point.
- Keep full-screen takeover copy above the subtitle band with stable width and predictable wrapping.
- Use unframed full-bleed scenes for major moments. Cards are for repeated evidence items, not page-section decoration.

## Evidence Treatment

For screenshots and screen recordings:

1. Establish the full interface for `0.4-1.0s`.
2. Cut or animate into a meaningful crop, usually `2.5-3x` larger than the full-page view.
3. Add one plain-language callout that states why the highlighted region matters.
4. Use a marker, crop, underline, or bounded highlight. Do not place a generic glowing rectangle over the whole screenshot.
5. Exit before the viewer must read dense desktop UI at native scale.

Use real screenshots, charts, screen recordings, icons, and diagrams as evidence. Decorative stock imagery should not replace the product or workflow being explained.

## Motion

- Fast entrances: `0.18-0.56s`, usually `power3`, `power4`, `circ`, or `expo` easing.
- Slow evidence movement: `2-7s` crop pan or scale drift.
- Use composition changes and asset takeovers for energy; do not simulate energy with constant shaking or flashing.
- Make each transition explain a relationship: source to result, tool to tool, parameter to value, prompt to preview, problem to revision.
- Limit transition families to hard cut, short masked wipe, position/scale handoff, and a restrained fade where needed.

## Audio

- Default BGM: none.
- Preserve source speech at full level.
- Use sparse SFX only on visible landings such as title lock, data scan, approval, export, or final thesis.
- Reuse a small sound vocabulary. For a two-minute tutorial, `6-14` cues are normally enough.
- Keep SFX short and at least `12dB` below speech peaks; avoid a sound on every chapter boundary.
