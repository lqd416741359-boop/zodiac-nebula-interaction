# Design Pattern: Fingertip Starfield to Capricorn Reveal

## Four gestures, one ordered show

| Gesture | Action | Trigger rule |
| --- | --- | --- |
| Index movement | Fine, short-lived stardust trail | Continuous while a hand is tracked |
| Pinch | Star cluster bloom at the fingertip | On stable entry; latch until released |
| Open palm | Broad nebula bloom at the palm center | On stable entry; cooldown prevents repeats |
| Thumbs-up | Start the multi-planet orbit | Exact pose classification; do not infer from pointing |
| V sign | Reveal Capricorn | Only after planets have been visible long enough |

The fingertip trail is the ambient interaction; the four named poses are discrete events. Keep pose events from retriggering every inference frame while the user holds a pose. Show the currently recognized gesture so users can correct their hand position.

## Capricorn reveal sequence

1. Start the orbits around a shared visual center, with planets traveling on visibly distinct circular or elliptical paths. Use different radii, speeds, phases, sizes, and restrained surface detail; avoid a single straight row or vertical track.
2. Keep the orbit active while the user holds the pose. Do not start the finale automatically after a timer; wait for the explicit V sign.
3. On V sign, settle or dissolve the planets into particles, then progressively draw a recognizable sea-goat silhouette/constellation and its major connecting stars.
4. Add the Capricorn glyph and the correctly spelled `CAPRICORN` wordmark as separate, clear layers. Let each resolve from fine points into a stable readable hold.
5. Hold the finished image for recording before resetting to the idle sky. If the user repeats a gesture, avoid accidentally dismissing the finale.

## Visual language

- Use a deep navy-to-black sky with layered, restrained star density and a soft violet-blue Milky Way band. Keep an idle background visible; summoned planets are transient effects.
- Build stars from varied pinpoints, subtle diffraction rays, and low-opacity halos. Reserve bright flares for a few key stars; avoid uniform glowing circles, dense blobs, and excessive cross-shaped flares.
- Keep star trails brief and directional. The user's hand should remain the source of the motion rather than leaving permanent scribbles across the frame.
- Render the Capricorn silhouette and lettering as intentionally designed geometry or sampled points from rights-cleared artwork; avoid placing an entire poster image over the live scene. Keep constellation lines thin and let key stars carry the contrast.
- Make effects conspicuous enough for a phone recording while preserving negative space around the central reveal.

## Pose and tracking notes

MediaPipe Hand Landmarker reports normalized landmarks. Classify fingers using joint geometry relative to the hand scale, not only whether a fingertip is higher on screen; the camera angle and rotated wrist change screen-space direction. Derive a stable pose after a few consecutive matching frames, and use distinct thresholds for pinch distance and thumb extension. Test the open palm, pinch, thumbs-up, V sign, and nearby confusable poses under mirrored preview conditions.

Map the mirrored index-tip coordinate to the Canvas scene for the trail. Use a smoothed coordinate for visual motion, but keep the smoothing modest so the trail follows without visible lag. Draw a 21-point hand skeleton only in the camera preview if the user wants tracking feedback; do not put the skeleton over the celestial scene by default.

## Recording and resource checklist

- Provide an explicit start/stop camera control and a clear permission/error status.
- Preserve a mouse/touch path when no camera is available.
- Keep inference independent of particle-speed controls.
- Bound camera resolution and process only the newest frame when inference is busy.
- Stop tracks and workers on camera stop; resume cleanly after tab visibility changes.
- Test startup, denied permission, missing camera, model load failure, gesture entry/release, planet-to-Capricorn order, and reset.
- For Douyin/TikTok capture, compose for a portrait canvas and keep labels away from platform overlays and browser chrome. Let the user start the recording; do not automate publishing.
