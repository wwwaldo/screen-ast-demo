# screen-ast-demo — country dropdown benchmark

A tiny, self-contained **computer-use benchmark**: select **United States** in a dropdown,
across three difficulty tiers on one page —

- **native** `<select>` (easy)
- **custom** scrollable div listbox (must scroll)
- **virtualized** listbox (off-screen options aren't even in the DOM until scrolled near)

The target sits ~95% down an alphabetical list of 195 countries, so naive scroll-hunting is
slow. The interesting question: does the agent *recognize the ordering and jump*, or crawl?

**Live:** https://wwwaldo.github.io/screen-ast-demo/

## Try it with a browser-use agent

Point any computer-use agent at the URL and ask it to select **United States** in each of the
three dropdowns. The page instruments itself so you can score the attempt.

### Scoring API — `window.FIXTURE`

- `target` — the country to select (`"United States"`)
- `solved` — `null` until solved, then `{ variant, value, actions, opens, scrolls, ms }`
- `telemetry` — `{ actions: [{type, detail, t}], opens, scrolls }`
- `indexOf(name)` — alphabetical index of a country
- override the target with `?target=Japan`

Interaction types recorded: `open`, `scroll`, `select`, `solved`. Read `solved.actions` /
`solved.ms` to compare an agent against the anchors: an oracle `page.select()` (~ms), a human
(~15s), and a current pixel-scrolling agent (~2min).

Self-contained static HTML — no build, no dependencies.
