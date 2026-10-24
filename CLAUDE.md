# You, Inc.

A habit app where you're a public company ($CAL). The spec is the Claude Doc "You, Inc. — Habit App Spec" (https://claude.ai/artifact/AbrzSSsstNmiokok6tgxhR).

## Current state

Spec build phase 1, plus a plain (non-staged) earnings call so the week can settle. Single-file PWA, the same pattern as `tape-wall`: `index.html`, `manifest.json`, `sw.js`, `icons/`. All state is one localStorage key (`youinc-v1`), with export/import JSON in Setup. Dev server: `you-inc` in `VibeHouse/.claude/launch.json` (port 8936).

Hosted on GitHub Pages at https://calmac300-cmyk.github.io/you-inc/ from `main` / root of the public repo `calmac300-cmyk/you-inc`. Pushing to `main` deploys. The service worker is network-first, so the phone picks up a new version on its next online open.

Defaults chosen for the spec's open questions [2026-10-23]:
- The week runs Saturday to Friday. The call opens Fri 6pm and auto-reports Mon 9am. Anything logged before you hold the call counts for that week.
- All segment weights are 1, and they're editable in Setup.
- Fund lines are hand-written templates in `LINES`. No LLM, no Discord.

Deviations from the spec:
- Intraweek drift uses `share × (pace − 1)` (a deficit as a fraction of guidance) instead of raw pace, so Monday morning doesn't open deep red.
- Baselines are normalized by week length, so a short IPO week doesn't drag them down.
- Positions and smugness are derived from logs rather than stored.

Not built yet: the staged call reveal, trophy wall, weekly candles, short squeezes, desktop ticker tape, ticker.json/KWGT, and the native layer (phases 2 to 4).
