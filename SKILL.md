---
name: jitter-motion
description: Build and revise editable UI walkthrough animations in Jitter from designs and motion references. Use for Jitter timelines, gestures, transitions, changing content and numbers, and export compression; not for static UI design.
---

# Jitter motion

Build an editable interaction sequence that communicates the product clearly. Match the supplied design and motion reference; the user's timing and scope override the defaults below. These principles apply across interfaces, not just messaging apps.

## Working environment

- For this user's Figma → Jitter workflow, use **native Figma desktop** for the plugin export and **Codex's in-app browser** for the Jitter editor. Apply the latest explicit user instruction if a different surface is requested; do not carry an older browser choice over a newer correction.
- **Never create a new Jitter project/file, including temporary staging files. Work only in the Jitter files supplied by the user.** References may be read and copied from but are not destinations to modify. Import into the supplied destination; do not use an Open in Jitter action that creates a separate file.
- Identify the source Figma file and authorized destination Jitter file before acting. When continuing earlier work, recover relevant environment instructions before starting the export, not after choosing a workaround.
- Figma MCP can inspect layers and prepare export copies, but export through **Jitter · Animation for Figma in native Figma**. Do not replace that step with the Figma web app.
- Native and in-app browser clipboards are separate. Bridge the plugin export into the authorized existing file. If the available import route would create a new project, stop that route and find a supported paste into the existing file; do not create a staging project.
- If another task changes an app, refresh its state and check the intended file before continuing. Do not compete for control or silently switch the user's selected working surfaces. Report a concrete blocker when the required surface cannot be used.

## Source and structure

- Establish the authorized destination, source designs, and references. References are component sources, not destinations to modify. Use connectors or documented UI controls within the required working environment above; do not assume a private API exists.
- Import editable design layers through the available Figma/Jitter workflow. Check fonts, bounds, clipping and effects before composing motion. Preserve original artwork; raster assets are appropriate for supplied photos or rendered effects.
- If Figma → Jitter export rasterizes an editable element with a warning such as “remove corner smooth radius”, set that element’s corner smoothing in Figma to 0% (for example, replace 60% with 0%), then export/import it again. Preserve the actual corner radius and confirm that Jitter receives an editable vector rather than a PNG. Do not accept rasterization as the workaround for corner smoothing.
- If editable inputs or controls rasterize because of multiple shadows, duplicate them in Figma, remove the drop/inner shadows from the export copies, and import through the native plugin. Recreate the original shadows manually in Jitter, preserving offsets, blur, colors and opacity. Never combine background blur and a shadow on the same Jitter layer: this causes a rendering bug. Use separate synchronized layers for the backdrop blur and vector control/shadow. Verify the container remains a vector/group with editable children, not a fallback PNG; supplied thumbnail photos may stay images. Preserve original Figma artwork.
- Organize layers by persistent function: navigation, fixed controls, scrolling viewport and content, changing content, transition elements, gesture indicators. Do not construct an interaction by stacking complete copies of every screen.
- Reuse shared controls and their actual layers/effects. Keep persistent chrome separate from moving content. Group related elements around the coordinate system in which they move.
- Use one layer in Layers for a recurring element or event; put its repeated appearances in Animation. For example, reuse one “Memory updated” notice for every update instead of creating a notice layer per event. Give each occurrence its own named animation group targeting the same layer, and restore its hidden/resting state between occurrences. When consolidating existing duplicates, preserve appearance and timing, retarget all operations, and remove unused layers only after checking the complete sequence.
- Group timeline operations by meaningful action, with gesture, control response and dependent movement together. Name groups so the owner can retime a whole action without separating synchronized parts.
- Name each Jitter artboard **`Feature name · HH:MM`**, using the feature's actual name and the current time in **Europe/Moscow** when creating that version. For example, `News · 18:48`; News is an example, not a required prefix. Do not add technical version counters or scenario suffixes unless the user asks.
- Keep the canvas legible: current scenarios aligned chronologically from left to right, new versions to the right of earlier versions, and references in separate rows. Preserve earlier versions when requested.

## Gesture behavior and alignment

- Reuse the project's Tap indicator, including fill, transparency, blur and scale behavior. Do not impose a universal ring size or color.
- Center Tap on the actual control at the time of interaction, using the transformed parent coordinates and half the indicator's dimensions. Recheck after resizing, moving or scaling a parent. Visual alignment of chevrons/icons may differ from their bounding-box center; compare the source design.
- On press, scale the actual button to **90–98%**, choosing by its original size: small icon buttons closer to 90–94%, medium buttons around 95–97%, large controls around 98%. Animate that control separately from the Tap indicator and restore it to 100% on release. A Tap indicator alone is not button feedback.
- For a fully clickable card, scale the whole visible card (image, title and text), with bounds matching its current visible state. Do not apply press feedback only to the thumbnail.
- On press, compress the indicator and the appropriate control; on release, restore them and trigger the response without an unexplained idle gap. A roughly 150–200 ms press/release is a starting point when no reference is supplied.
- During a drag, hold the pressed state and move the indicator, thumb and active track together. Use one continuous movement per direction, not a sequence of tiny moves. Release after the drag sequence. A grabbed indicator/thumb generally gets smaller, not larger, unless the reference specifies otherwise.
- For scrolls, use a scroll indicator based on the project’s reference Tap component, preserving its appearance and reference press/release behavior. Start with exactly the ordinary Tap scale-in and stronger press compression; hold that pressed scale during the continuous drag, then use the ordinary Tap release scale-out and fade. The only difference from a normal tap is movement in the middle. Synchronize the indicator’s continuous drag with the moving content; content movement alone is insufficient. Keep fixed chrome stationary and synchronize gesture with content. Avoid a dead interval between capture and movement. Adjust only the requested scrolls; a scroll timing request does not authorize retiming taps or slider drags.

## Tempo and easing

- Use Smooth as the starting easing for UI motion, including slider travel and rolling digits. Follow an explicit reference if it uses a different curve. Keep synchronized properties on matching curves and durations; mixed curves can make the indicator drift from the control.
- Separate animation duration from reading hold. Measure a hold from when content is fully visible, not from the start of its entrance. Short text may need about 1–2 s; dense content often needs 2–4 s. Choose by reading load and the purpose of the demo, not one global pause.
- When accelerating a walkthrough, shorten idle gaps first. Preserve gesture feedback and legible transitions unless explicitly asked to change them. State actual changed durations when useful.
- A fast skip should read as a deliberate change of pace: accelerate connected content smoothly, keep fixed anchors, then settle clearly on the next important state. Use a short explicit context marker when the scenario changes purpose.
- A subtle attention pulse may emphasize a newly important state. Avoid repeating it on the return transition unless requested.

## Changing content inside one cell

- Keep one persistent container. Animate its background and replace its inner content, rather than overlaying another complete card or screen.
- Use a synchronized short transition: outgoing content moves a few pixels, fades and blurs; incoming content settles from the opposite offset, sharpens and fades in. About 250–350 ms is a useful starting point, not a fixed rule. Keep padding and settled position identical in both directions.
- Define each state's resting position and accumulated relative moves. A reversal must start from the current position, not jump to an unrelated explicit start value. Verify forward, reverse and repeated transitions; checking only the final frame misses discontinuities.
- After changing text, resize the text bounds and containing cell as needed. Update subsequent layout positions and dependent animation distances together. Do not leave the old multi-line height around a shorter message.
- For bottom-anchored feeds, new content enters from the bottom and pushes existing content upward. Keep associated avatars or markers in the intended stationary/moving group; show them with their first relevant content. Apply this only to interfaces using that behavior.

## Number changes

- Split the formatted value into digit columns; keep separators, spaces and units stable. Use monospaced digits or tabular figures to avoid horizontal jitter.
- Animate only changing places, including carries/borrows. Use clipped digit columns with rolling movement and a brief blur that resolves at each settled value; do not rotate or slide the entire amount as one text layer.
- Coordinate value steps with the continuous slider. Choose a useful increment for the domain; do not hard-code 500 or 1000 for every product. For nonlinear slider easing, place thresholds according to the eased travel so the displayed value tracks the thumb.
- Reverse the rolling direction consistently and preserve final alignment. Check changing leading places and boundary crossings, not only a single digit.

## Verification and delivery

- Inspect the start, middle and settled end of changed actions, then play the connected sequence to judge tempo. A screenshot cannot verify easing or reading time.
- Check clipping, layer order, shared-control alignment, gesture centers, forward/reverse continuity and later dependent movements. Video layers need playback operations as well as assets; seeking may show an unloaded frame, so check playback before declaring an asset missing.
- Verify the pasted/edited timeline actually retains its animations and saves. For native clipboard composition, read [references/native-clipboard.md](references/native-clipboard.md).
- **Default delivery is the Jitter canvas.** Select the current artboard, show it in the authorized browser, provide its scene link, and leave it available for the user to inspect. Do not start exports or compression while the user is reviewing or iterating.
- Start **export and compression only after the user explicitly says these are the final passes** (for example, “финальные заходы”) or explicitly authorizes final export now. A request to see the animation or an earlier urgent request for a video does not override a later canvas-review instruction. Then read [references/video-compression.md](references/video-compression.md).
- Provide a useful verification screenshot with the scene link.
