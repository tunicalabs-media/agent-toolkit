# React Native Best Practices

## Download Source
`npx skills add https://github.com/callstackincubator/agent-skills --skill react-native-best-practices`

## What This Skill Does
React Native Best Practices provides performance optimization guidance for React Native applications. It targets FPS, time to interactive, bundle size, memory leaks, re-renders, animations, native modules, platform setup, and native profiling workflows.

## Features
- Priority-ordered optimization workflow for JS, native, and bundling concerns.
- Reference mapping for symptoms such as jank, bridge overhead, memory growth, slow startup, and large bundles.
- Supporting images and reference files for profiling tools, bundle analysis, and architecture patterns.

## Typical Use Cases
- Diagnosing frame drops, slow startup, or sluggish interactions.
- Reviewing React Native code for memory leaks, uncontrolled components, or list performance.
- Optimizing Hermes, native modules, app bundles, and platform-specific setup.

## Files Included
- `SKILL.md` - Main onboarding and guideline index.
- `POWER.md` - Alternate/power-user onboarding and reference mapping.
- `agents/` - Agent configuration for OpenAI-style usage.
- `references/` - Detailed performance notes and supporting images.

## Notes
Several references include platform-specific commands and tooling expectations. Validate against the target app’s React Native, Expo, Android, and iOS setup before applying changes.
