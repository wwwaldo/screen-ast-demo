# screen-ast-demo — computer-use benchmarks

A small suite of self-contained **computer-use tests**. Point a browser-use agent at one and
score how it does — each page instruments itself on `window.FIXTURE`.

**Live:** https://wwwaldo.github.io/screen-ast-demo/ (sidebar picks the test)

## The tests

| Test | Direct URL | What it probes |
|---|---|---|
| **Country Dropdown** | [`/country-dropdown.html`](https://wwwaldo.github.io/screen-ast-demo/country-dropdown.html) | Select "United States" in a dropdown across 3 tiers (native / custom / virtualized). Target ~95% down a 195-item alphabetical list — does the agent *recognize the ordering and jump*, or scroll-hunt? |
| **Workday Form** | [`/workday-form.html`](https://wwwaldo.github.io/screen-ast-demo/workday-form.html) | Fill a Workday-style application: **15-deep div-soup**, all-custom div widgets (no native `<select>`/radios), **dependent** country→state, and a **state-gated submit** (`aria-disabled` until required present). A DOM-walker drowns; vision sees a clean form. |

Each test is reachable at its own clean URL (so an agent gets top-level `window.FIXTURE`), and
the root page is a sidebar shell to browse them with a "Check result" button.

## Scoring — `window.FIXTURE`

Common:
- `target` — what to achieve
- `solved` — `null` until solved, then a result object (`{ ..., actions/ms/... }`)
- `telemetry` — recorded interactions (`open`, `scroll`, `select`, `type`, `submit`, …)
- `reset()` — reload

Country Dropdown adds: `countries`, `indexOf(name)`, `?target=Japan` override.
Workday Form adds: `required`, `values()`, `check()` (per-field correctness vs the target profile).

Compare an agent's `solved.ms` / action count against the anchors: oracle `page.select()` (~ms),
a human (~15s), a current pixel-scrolling agent (~2min).

Self-contained static HTML — no build, no dependencies.
