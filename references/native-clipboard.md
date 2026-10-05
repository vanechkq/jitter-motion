# Native clipboard editing

Use only data obtained through the application's normal Copy action. The following are observed Jitter invariants; verify them against a fresh copy if the format changes.

- Copied artboards use `{layers: [root], operations: []}`. Trees hold nodes with `id`, `item`, and optional `children`; operations reference `targetId`.
- For a new duplicate, remap every node ID and all operation targets consistently. Keep the layers tree before the operations tree when composing an artboard.
- Omit empty `children: []` on leaves and operations. Some imports appear successful while silently dropping operations when these are present.
- Paste an artboard with nothing selected; otherwise it can become nested. The application may place it at the paste location despite stored x/y. Set its canvas position through the UI afterward.
- Move operations without `fromValue` are additive. Explicit starting values can alter pre-animation state. Compute accumulated offsets before adding a reversal; avoid a discontinuous starting offset.
- Native rotation uses `rotate`; do not invent an `angle` operation. Preserve actual schemas and easing data from the copied reference.
- A copied video requires its `playVideo` operation. Keep its offset, duration and target intact. SVG/vector text may be exported as a remote asset URL rather than an inline data URL.
- Re-copy the pasted artboard. Compare operation counts/types, resolve every target, and check modified durations and easing. Then verify visually in playback; structural checks alone are insufficient.
