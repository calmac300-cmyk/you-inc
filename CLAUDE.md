# You, Inc.

A habit app where you're a public company ($CAL). The spec is the Claude Doc "You, Inc. — Habit App Spec" (https://claude.ai/artifact/AbrzSSsstNmiokok6tgxhR).

## Current state

Spec build phase 1, plus a plain (non-staged) earnings call so the week can settle. Single-file PWA, the same pattern as `tape-wall`: `index.html`, `manifest.json`, `sw.js`, `icons/`. All state is one localStorage key (`youinc-v1`), with export/import JSON in Setup. Dev server: `you-inc` in `VibeHouse/.claude/launch.json` (port 8936).

Hosted on GitHub Pages at https://calmac300-cmyk.github.io/you-inc/ from `main` / root of the public repo `calmac300-cmyk/you-inc`. Pushing to `main` deploys. The service worker is network-first, so the phone picks up a new version on its next online open.

Defaults chosen for the spec's open questions [2026-10-23]:
- The week runs Saturday to Friday. The call opens Fri 6pm and auto-reports Mon 9am. Anything logged before you hold the call counts for that week.
- All segment weights are 1, and they're editable in Setup.
- Fund lines are hand-written templates in `LINES`. No LLM, no Discord.

Added past the spec [2026-10-24]: a fifth fund, Bedhead Holdings, shorting a "Getting ready" daily segment (shower/shave/skincare as one tap), with a "Slept in" disclosure. `migrate()` pushes any `DEFAULT_SEGMENTS` entry missing by id into existing installs, so new default segments reach the phone without a reset.

Deviations from the spec:
- Intraweek drift uses `share × (pace − 1)` (a deficit as a fraction of guidance) instead of raw pace, so Monday morning doesn't open deep red.
- Baselines are normalized by week length, so a short IPO week doesn't drag them down.
- Positions and smugness are derived from logs rather than stored.

Built since [2026-11-09]: short squeezes, which are derived from logs and never stored. A good-day streak in a habit squeezes on day 3, 5, 7..., giving +1.5%, smugness −15, position ×0.8 and fund P&L −1.5. Sandbagged guidance (B < 0.9) can't squeeze. Also weekly candles on the Funds tab, and every logged data point now gets a fund reaction (`REACTIONS`).

Deliberately skipped, since the user felt they'd crowd the app [2026-11-09]: the trophy wall and a morning pre-market note.

The board [2026-11-23] is for free time. It's a single "Convene the board" button on the Floor, deliberately not a separate screen.
- **Picking the block:** you choose 15, 30 or 60 minutes. Three shareholders vote on a habit. Prudence backs the one furthest behind pace. Rex backs one near a squeeze, otherwise the boldest. Nana backs the most neglected one. On a tie, Rex and Nana vote away from Prudence's pick. The majority wins; otherwise Prudence chairs.
- **What can't be picked:** cap habits, habits marked `board: false` (Nutrition and Getting ready, since one block of time can't move them), and once-a-day habits already done today.
- **Running the block:** the countdown is clock-based, so it survives reloads. Done unlocks when time is up. It logs the habit's day (or +1 for count habits), pays a bonus (`board` log: +0.5%, +1% or +2%) and earns 1 proxy.
- **Countermanding** picks another habit instead. It spends a proxy, or costs 2% if you have none (`countermand` log), and earns no proxy. Abandon costs nothing but a board line.
- State lives in `S.proxies` and `S.block`. Board posts are feed entries with a `board` member id.

Not built yet: the desktop ticker tape, ticker.json/KWGT, and the native layer.
