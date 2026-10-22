# HyperFrames + GSAP skills for Codex

Three compact, independently authored skills for HTML/GSAP video creation. Tested CLI baseline: HyperFrames 0.8.185, GSAP 3.14.2, Node.js 24, Chromium and FFmpeg on Linux.

## Install

Copy `.agents/skills/` to your repository root, preserving the three subdirectories. Alternatively extract `HyperFrames_GSAP_Codex_Web.zip`. Start a new Codex task to discover the skills, or explicitly ask Codex to read their SKILL.md files.

Example: “Use the HyperFrames and GSAP skills to create a 16:9 animation of chromosome condensation with Vietnamese annotations. Check and render MP4, then deliver the video through the client's supported artifact mechanism.”

## Codex compatibility

- Node.js >=22, Chromium, FFmpeg and FFprobe are required for rendering.
- CLI tools, npm cache and preview state use writable workspace paths; no assumptions about a writable home directory.
- Pinned CLI version; `hyperframes check` replaces deprecated `validate` and `inspect`.
- Local GSAP/fonts avoid browser CDN certificate and network failures without disabling TLS verification.
- Check real command output, inspect scene snapshots and verify the rendered file with FFprobe.
- Workspace source links and localhost addresses do not guarantee remote video playback. Use supported attachments/downloads; sandbox links depend on the client. No automatic external publishing.
- Optional speech, transcription and music dependencies are not required for silent rendering.

The ZIP contains exactly this README and the three skill files. It is not an installed CLI or a complete upstream skill collection. Environment preparation and successful local rendering do not establish that every Codex client supports downloading the output.

Upstream: https://github.com/heygen-com/hyperframes
