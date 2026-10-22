---
name: hyperframes-cli
description: Scaffold, lint, preview and render HyperFrames videos with the CLI.
---
# HyperFrames CLI
Prerequisites: Node.js >=22 and FFmpeg.
```bash
npx hyperframes init my-video --non-interactive
cd my-video
npx hyperframes lint
npx hyperframes validate
npx hyperframes inspect
npx hyperframes preview
npx hyperframes render --output final.mp4
```
For diagnostics use `npx hyperframes doctor`. For high-quality output use `npx hyperframes render --fps 60 --quality high`.
The web Codex environment may need dependency setup and may not support video rendering until Chrome/FFmpeg are available.
See https://github.com/heygen-com/hyperframes
This is a compact, independently authored reference, not a complete upstream copy.
