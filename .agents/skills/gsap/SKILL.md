---
name: gsap
description: Use GSAP timelines and tweens to animate HyperFrames compositions.
---
# GSAP for HyperFrames
Use `gsap.from()` for entrances, `gsap.to()` for exits and `gsap.fromTo()` for explicit animation.
Prefer `x`, `y`, `scale`, `rotation`, `opacity` over layout properties.
Use `gsap.timeline({ paused: true })`, then register the timeline in `window.__timelines`.
Use time positions (`0`, `"<"`, `"+=0.3"`) and labels to sequence animations.
Example:
```js
window.__timelines = window.__timelines || {};
const tl = gsap.timeline({paused:true});
tl.from(".title", {y:60, opacity:0, duration:0.8, ease:"power3.out"}, 0.2);
tl.from(".subtitle", {x:-30, opacity:0, duration:0.6, ease:"expo.out"}, 0.5);
window.__timelines["main"] = tl;
```
Never use infinite `repeat:-1` in HyperFrames render timelines.
See https://gsap.com/docs/v3/ and https://github.com/heygen-com/hyperframes
This is a compact, independently authored reference, not a complete upstream copy.
