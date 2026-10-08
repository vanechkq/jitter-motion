# Export and compression

Before starting an export, check the delivery gate in `../SKILL.md`. During review, show the canvas. Start export and compression only after explicit final-pass or final-export authorization.

When asked to wait for an export, inspect the actual export tabs and download each completed result. Avoid restarting an export already underway. Keep working until the requested files are downloaded, processed and verified.

For ordinary opaque UI videos, a useful starting point is MP4/H.264, CRF 23, preset slow, yuv420p and faststart. Preserve source dimensions and frame rate unless the user requests smaller output or a size constraint requires a tradeoff. Preserve audio when present; AAC 128 kb/s is a reasonable starting point. Use a reputable existing FFmpeg runtime or package.

For transparent assets, use a format and encoder that preserve alpha (for example WebM/VP9 with appropriate alpha support), and verify transparency. Ordinary H.264 MP4 loses it.

Write new descriptive filenames without overwriting originals. Verify complete decode, duration, dimensions/frame rate, output size and representative frames. Report actual sizes and any quality/resolution tradeoff. Save to the requested location and provide file links.
