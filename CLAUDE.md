# YAPS — notes for Claude

Single-file browser population simulator for a non-technical user. Live at
https://op12no2.github.io/yaps/ (GitHub Pages, root of `main`). Repo:
github.com/op12no2/yaps. Read `README.md` for what the app does and how the
model works; this file is about how to work on it.

## Files

- `index.html` — the whole app: CSS, markup and JS in one file. No build step,
  no dependencies except two Google Fonts (with system fallbacks).
- `README.md` — user-facing documentation. Keep it in step with every feature
  change; it is written for the non-technical user, not for developers.
- `LICENSE` — MIT.

## Every push

1. **Bump the version badge** in `index.html` (the `.ver` span in the header,
   `v1.0` → `v1.1` …). One bump per push. GitHub Pages lags a minute or so
   behind and the badge is how the user tells whether they are looking at the
   latest build.
2. Put the new version at the start of the commit message, e.g.
   `v1.4: retirement age up to 120`.
3. Push straight to `main`. There are no branches or PRs on this project.

## Design rules (the user's, and they matter)

- **KISS.** One population, one chart, one file. Resist adding structure.
- **No typing.** Every input is a slider, a button, or a drag-point graph.
  Never add a text or number field.
- **No modal dialogs.** `confirm()`, `prompt()` and `alert()` are silently
  blocked in sandboxed frames and made Reset look broken once. Use the
  two-click pattern (see Reset) or a toast.
- **Dark theme only.** Colours are CSS tokens on `:root`; don't add a light
  theme or media queries for colour.
- **One chip active at a time** on the chart, each with a real axis. Never
  overlay measures with different units on one axis (that was tried and
  reverted).
- **Section headings** in the panel are bold uppercase and clickable (they
  open the graph full size). Keep preset buttons out of the panel; the graphs
  are the interface.
- The user explicitly invites push-back on design ideas. Give it in a sentence
  or two, then build what they ask for if they reaffirm.

## Model notes

- Cohort model, single-year ages 0..170 (`AGES = 171`), so life expectancy up
  to 150 works. Mortality is Gompertz-Makeham with an infant bump, solved by
  bisection to hit the life-expectancy graph; cached per 0.1 year.
- Every time-varying input is a list of `{t, v}` points, `t` in 0..1 across the
  horizon, joined by a monotone cubic (`interpolator`). The age profile uses
  the same editor with `t` mapped to age 0..`AGE_MAX` (150).
- Working-age and retirement boundaries are fractional: the cohort each falls
  inside is split proportionally. Don't round them, it causes sawtooth
  artefacts in the ratios.
- The MVP ratio is retired ÷ working-age; threshold 1.0; higher is worse.
- The model never reads the clock. `state.year0` is a label offset only.

## State and compatibility

- `state` is saved to `localStorage` (`yaps.v2`) and packed into the share
  link hash as base64 JSON. `valid()` migrates older shapes (missing curves,
  numeric retirement age, 100-wide age axis). When you add a field, add a
  migration line there so existing saved set-ups keep working.
- `state.ageMax` records the age-axis width the profile was drawn against.

## Checking a change

- Syntax: extract the script and `new Function(js)` it in node.
- Model numbers: the demography section (from `const AGES` up to
  `// ---------- state ----------`) runs standalone in node; write a scratch
  file that appends a `simulate(...)` call and print what you need.
- Rendering: headless Chrome is available at
  `~/.cache/ms-playwright/chromium_headless_shell-*/.../chrome-headless-shell`;
  `--screenshot` with `--virtual-time-budget=4000` on the local file. To open
  a specific state, base64 a JSON state into `#s=` on the URL. To open the
  full-size editor, append a `setTimeout(() => enterFocus('fert'), 300)` in a
  scratch copy.
- The artifact preview is `index.html` with the doctype/html/head/body wrapper
  stripped (`<title>`, `<link>`, `<style>` first, then the markup and script).
