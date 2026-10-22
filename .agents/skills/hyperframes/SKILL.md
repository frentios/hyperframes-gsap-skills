---
name: hyperframes
description: Create HTML-based video compositions with GSAP animation, captions, scene transitions, audio and media.
---
# HyperFrames — Codex Skill
Use for HTML-based video creation, animation, titles, overlays and captions.
## Workflow
1. Define DESIGN.md (palette, typography, motion rules) before writing compositions.
2. Design each scene's final visible layout in HTML/CSS first.
3. Use `data-composition-id`, `data-width`, `data-height` on the root composition.
4. Use `data-start`, `data-duration`, `data-track-index` for timed clips.
5. Animate entrances with GSAP and register a paused timeline as `window.__timelines[compositionId]`.
6. Add transitions between scenes; avoid infinite repeats or random/time-dependent animation.
7. Run `npx hyperframes lint`, `npx hyperframes validate`, `npx hyperframes inspect`, then `npx hyperframes render`.
## Key rules
- Root composition goes directly in body, not in a template.
- Use `data-track-index`, not `data-layer`; `data-duration`, not `data-end`.
- Keep video muted and audio on a separate audio track.
- Never create timelines asynchronously or call play/pause on media.
- Animate transforms and opacity, not layout dimensions.
## Full upstream skill
https://github.com/heygen-com/hyperframes
This is a compact, independently authored Codex skill based on available HyperFrames guidance, not a complete mirror of upstream reference files.
