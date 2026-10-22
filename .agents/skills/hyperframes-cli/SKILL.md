---
name: hyperframes-cli
description: Set up, check, preview and render HyperFrames videos in Codex, including writable caches, local assets and artifact delivery.
---
# HyperFrames CLI in Codex

Read the project's AGENTS.md and preserve existing files. Use the current checkout; do not create a worktree unless requested. Check installed tools before installing anything. Requires Node.js >=22, FFmpeg/FFprobe and a Chromium-compatible browser. No API key is needed for local HTML/GSAP rendering. Speech, transcription and music generation are optional and have separate requirements.

## Prepare a writable tool directory

Run from the repository root. These paths are examples under the current writable workspace, not assumptions about `/home`, `/mnt/data`, or another machine. Reuse a working installation if one exists. Keep tools outside tracked source and do not change application lockfiles just to install the CLI.

```bash
export HF_TOOLS="$PWD/.hyperframes-tools"
export npm_config_cache="$PWD/.npm-cache"
export XDG_STATE_HOME="$PWD/.hyperframes-state"
export HYPERFRAMES_NO_TELEMETRY=1
mkdir -p "$HF_TOOLS" "$npm_config_cache" "$XDG_STATE_HOME"
node --version
ffmpeg -version
ffprobe -version
# Compatibility baseline tested in Codex; do not silently install latest.
npm install --prefix "$HF_TOOLS" --no-audit --no-fund hyperframes@0.8.185 gsap@3.14.2
export PATH="$HF_TOOLS/node_modules/.bin:$PATH"
# Set this only after locating an actual executable; path varies by machine.
# export HYPERFRAMES_BROWSER_PATH=/usr/bin/chromium
hyperframes --version
hyperframes doctor
```

Reuse the tool directory's lockfile with `npm ci --prefix "$HF_TOOLS" --no-audit --no-fund` for subsequent installs. Exclude local tool/cache/state directories from commits. Keep these exports in the same shell or repeat them in later shell calls; shell state does not necessarily persist between tool calls. Never repurpose HOME or disable TLS, package signatures or checksums. Some CLI history/font caches still use the home directory; report residual warnings accurately rather than claiming all caches moved.

## Create, validate, render

```bash
# The repository already supplies compact skills. Skip automatic skill updates
# to avoid modifying agent instructions or requiring another registry.
HYPERFRAMES_SKIP_SKILLS=1 hyperframes init my-video --example blank --non-interactive
cd my-video
# Replace the scaffold's GSAP CDN reference with a local asset.
cp "$HF_TOOLS/node_modules/gsap/dist/gsap.min.js" ./gsap.min.js
# Edit index.html to load <script src="./gsap.min.js"></script>.
# Author the composition, then:
hyperframes check
hyperframes snapshot --at 1,4,7 --no-end --output snapshots
hyperframes render --output final.mp4 --quality standard --fps 30 --workers 1
ffprobe -v error -show_entries stream=codec_name,width,height,nb_frames -show_entries format=duration,size -of json final.mp4
```

`check` replaces the deprecated `validate` and `inspect` commands in this baseline. Read actual output as well as exit status. Choose snapshot times within the real duration, including each scene, motion and transitions; open and inspect the images. Fix errors, review warnings, and rerun affected checks after edits. Preserve command exit status when logging. Start with one render worker; increase only when resources permit. Regular Chromium may use slower software/screenshot capture; this can still render valid video. Missing optional voice/music tools do not block silent video. Report whether sound was produced.

Use local GSAP, fonts and other assets for repeatable renders. CDN certificate errors do not justify disabling TLS: use a verified package download or supported trust setup. Do not assume arbitrary font or media hosts are reachable.

## Preview and deliver

When a preview is needed, run `hyperframes preview --port 3017` from the project directory with the exports above. Version 0.8.185 starts a background preview by default. Verify its output and make a local HTTP request; stop only previews you started with `hyperframes preview /absolute/project/path --stop`. For another CLI version, inspect `preview --help` instead of assuming background flags. Live processes do not survive environment restoration reliably.

For remote Codex users, localhost is not a reachable preview. Use a platform-supported forwarded URL only when available and actually verified. Cloud onboarding does not support user-facing localhost previews.

Deliver the MP4 using an available artifact/attachment tool when supported. If the client supports sandbox downloads, use a link such as `[Download MP4](sandbox:/absolute/path/to/final.mp4)` with the actual existing artifact path. A plain workspace source link is not proof that the user can download or play video. Verify the delivery capability; never claim an attachment was uploaded or a link works without evidence. If download/attachment is unavailable, state that limitation and provide a source ZIP plus exact local render instructions using the supported transfer method. Do not publish externally unless explicitly authorized. Do not keep repeating a download link the user says is broken.

Upstream: https://github.com/heygen-com/hyperframes
Compact, independently authored reference; not a complete upstream copy.
