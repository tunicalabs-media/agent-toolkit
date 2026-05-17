# Remotion Best Practices

## Download Source
`npx skills add https://github.com/remotion-dev/skills --skill remotion-best-practices`

## What This Skill Does
Remotion Best Practices provides domain-specific guidance for creating videos with React and Remotion. It covers composition setup, frame-based animation, asset handling, sequencing, metadata, captions, audio, FFmpeg workflows, and render checks.

## Features
- Remotion-specific rules for using `useCurrentFrame`, `interpolate`, `Sequence`, and media components.
- Guidance for assets, captions, audio, video dimensions, metadata, and rendering.
- Detailed rule files for specialized video-production tasks.

## Typical Use Cases
- Building a new Remotion composition or video project.
- Adding captions, voiceover, sound effects, GIFs, Lottie, maps, or audio visualization.
- Debugging video timing, dimensions, transparent output, or render behavior.

## Files Included
- `SKILL.md` - Main Remotion workflow and required practices.
- `rules/` - Specialized references for captions, audio, video, FFmpeg, transitions, fonts, 3D, and more.
- `rules/assets/` - Reusable code examples for text animation and chart components.

## Notes
CSS transitions and CSS animations are explicitly discouraged for rendered video because Remotion output is frame-based.
