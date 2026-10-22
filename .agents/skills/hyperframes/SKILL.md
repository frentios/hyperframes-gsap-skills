---
name: hyperframes
description: Create HTML/GSAP videos in Codex with deterministic animation, Vietnamese labels, scene transitions, validation and downloadable output.
---
# HyperFrames — Codex Skill

Read the project's AGENTS.md and the companion hyperframes-cli and gsap skills. Treat requests to create a video as instructions to author, validate and render it, not just explain how. Use existing files and check git status before edits. For cloud onboarding alone, preserve tracked repository files; new video work is a separate authoring task.

## Workflow

1. Infer reasonable duration, resolution and style from the request. Ask only for missing details that prevent useful progress. For 16:9 use 1920×1080 by default. Use the user's language for captions; confirm fonts render Vietnamese diacritics when needed.
2. Write DESIGN.md with palette, typography, motion rules and constraints before composition HTML. Build each scene's fully visible layout first. Reserve space for labels and captions, then add animation.
3. Scaffold with the companion CLI workflow. Load GSAP and fonts locally; do not assume browser access to external CDNs.
4. Put the root composition directly in body, not a template. Include a unique id, data-composition-id, data-start="0", data-duration, data-width and data-height. Give timed clips unique ids, class="clip", data-start, data-duration and data-track-index. Use data-duration, not data-end; data-track-index, not data-layer. CSS controls visual stacking.
5. Register a synchronously constructed paused timeline as window.__timelines[compositionId]. Use deterministic, seekable animation. No random values, clocks, asynchronous timeline construction, infinite repeats or manual media playback.
6. Use transitions between scenes. Keep outgoing content visible until the transition starts. Limit each scene's duration to its actual interval, including transition overlap: do not leave all previous scenes active under later scenes. Hidden underlying text can cause genuine layout errors. Mark intentional overlap narrowly, never to conceal accidental collisions.
7. Use transforms and opacity for motion. Give reading text adequate size (around 28px or larger at 1080p) and contrast. Hold complex annotations long enough to read. Illustrations should demonstrate change, not just display different slides. Scientific diagrams must distinguish simplification from literal scale and avoid misleading mechanisms.
8. Run hyperframes check. Inspect snapshots of every scene and transition. Fix errors and inspect actual warning output. Do not treat a passing layout check as proof of correct appearance or scientific accuracy.
9. Render MP4 and verify codec, size, duration, dimensions and frame count with ffprobe. Deliver through the artifact/download mechanism in the CLI skill, with a concise description of duration, resolution and whether audio is included. Include editable source when useful.

Keep videos muted and audio on a separate timed audio track for this workflow. Do not add speech or music merely to silence a checker warning; use the user's request and available tools. Report silent output accurately. Never claim a render, preview, upload or check succeeded without running and verifying it.

Upstream: https://github.com/heygen-com/hyperframes
Compact, independently authored reference, not a complete mirror of upstream files.
