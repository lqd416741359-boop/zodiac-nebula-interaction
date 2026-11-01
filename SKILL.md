---
name: zodiac-nebula-interaction
description: Use when creating or revising a browser-based starfield, nebula, or zodiac experience controlled by hand gestures, especially a Capricorn finale with orbiting planets and a constellation reveal.
---

# Zodiac Nebula Interaction

Create a calm, cinematic starfield that responds to hand movement and builds toward a recognizable zodiac reveal. Treat the hand as a light brush: motion leaves delicate stardust, deliberate poses create distinct celestial events, and the finale resolves into a clear constellation rather than an unexplained particle cloud.

## When to use

Use for a desktop browser prototype or short-form-video experience involving MediaPipe hand tracking, stars or nebulae, orbiting planets, or a star-drawn zodiac symbol. The Capricorn sequence below is the reference direction; adapt the zodiac and gesture mapping when the user chooses another sign.

## Make the experience

1. Establish the visual target before adding motion. Preserve the user's selected galaxy palette and constellation shape. Ask for or create a reviewable still when the user wants visual approval first.
2. Build the idle sky and mouse/touch fallback before enabling the camera. Keep the camera preview and explicit **Start Camera** control visible. Request permission only after the user presses the control.
3. Make hand motion continuous and gesture actions discrete. Track the index fingertip for a short-lived, fine star trail; trigger an effect once when a stable pose is entered, with a latch or cooldown to prevent repeats.
4. Use the staged Capricorn show: **pinch** blooms a star cluster; **open palm** blooms a nebula; **thumbs-up** starts several planets on separate circular or elliptical orbits; after the planets have appeared and had time to read, **V sign** transitions into the Capricorn reveal. Do not reveal the sign from an open palm or during initial camera tracking.
5. Make the finale legible. Fade the planets into starlight, draw the goat/sea-goat constellation, connect the key stars, then reveal the Capricorn glyph and `CAPRICORN` wordmark. Hold the completed composition long enough to record, then reset intentionally. Use a user-provided or rights-cleared design as a guide; do not show a complete reference poster as a fake overlay.
6. Finish for the intended capture format. Keep controls legible, leave the central composition clear, expose a particle-speed control that does not change camera inference cadence, and support a vertical recording layout when requested.

## Browser and performance constraints

- Use a small static HTML/CSS/JavaScript/Canvas page unless the requested effect needs a larger rendering stack.
- Use MediaPipe Tasks Vision Hand Landmarker in the browser. Keep camera frames and landmarks local; do not add upload, analytics, accounts, keys, or backend services unless specifically requested.
- Initialize tracking only after permission. Prefer a Web Worker for inference, bounded camera resolution, one in-flight frame, and dropping stale frames instead of building a queue.
- Smooth pointer coordinates lightly. Keep the camera preview mirrored consistently with the hand overlay, and draw the 21 landmarks and connections only over that preview.
- Classify poses from relative landmark geometry and stabilize over consecutive frames. Test visually similar poses; a loose thumbs-up rule can misfire on pointing. Use cooldowns for sustained poses.
- Stop every media track and inference worker when the user stops the camera. Handle denied permission, missing devices, model/network failures, hidden-tab return, and no-hand detection with plain-language status and working mouse/touch fallback.
- Check the page through localhost or HTTPS for camera access. A `file://` page cannot reliably use `getUserMedia`.

## References

Read [references/design-pattern.md](references/design-pattern.md) for the sequence, pose mapping, rendering cues, and a compact completion checklist.
