---
name: gsap
description: Write deterministic, seekable GSAP timelines for HyperFrames video compositions in Codex.
---
# GSAP for HyperFrames

Load a locally installed, pinned GSAP asset before the composition script. Prefer x, y, scale, rotation and opacity over layout dimensions. Use gsap.from() for entrances and gsap.fromTo() for explicit states. Build the visible final layout in CSS first.

```js
window.__timelines = window.__timelines || {};
const tl = gsap.timeline({ paused: true });
tl.from(".title", { y: 40, opacity: 0, duration: 0.7, ease: "power3.out" }, 0.2);
tl.from(".subtitle", { x: -24, opacity: 0, duration: 0.6, ease: "sine.out" }, 0.5);
window.__timelines["main"] = tl;
```

The registration key must match data-composition-id. Construct synchronously; the player owns playback and seeking. Never call tl.play() or manually advance a timer for rendering. Use absolute positions, labels, "<" and relative offsets to coordinate motion. Do not use empty tweens just to set duration; use the composition's data-duration.

For scene transitions, animate the incoming scene over the outgoing scene, then let the outgoing clip end after the overlap. Do not fade its content away before the transition. Entrances on later-scene children must be scheduled inside their clip interval. Avoid gsap.set() on later timed clips at page load; use a timeline set at the relevant scene time when required.

Use immediateRender:false on later from/fromTo tweens targeting a property already animated earlier when needed to prevent initialization conflicts. Never animate the same property from competing timelines. Manually nested child timelines must not be paused; only the registered root is paused. Registered sub-compositions are nested by the framework, not manually added again.

Never use repeat:-1, Math.random(), Date.now(), setTimeout(), asynchronous timeline creation or video/audio play/pause calls. Finite repeats are allowed. Review snapshots at early, middle and late times, including seeking backward, to detect state that depends on playback order. Use opacity rather than visibility/display for animated fades.

References: https://gsap.com/docs/v3/ and https://github.com/heygen-com/hyperframes
Compact, independently authored reference, not a complete upstream copy.
