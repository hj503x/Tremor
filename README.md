# TREMOR — US Macro Event Console

A single-file reference tool for how US economic data releases and Fed
events typically move markets, plus a release calendar to know when
they're coming. Built for quick lookup before or during a trade — not
a live trading terminal.

## Two views

**Reference** — every major US macro event (CPI, NFP, PPI, PCE, FOMC,
ISM, JOLTS, housing data, and 30+ more) organized by category, each
with:
- Hot vs. cold market reaction — how USD, Treasury yields, and stocks
  typically move on a better- or worse-than-expected print
- Impact tier (Very High / High / Medium / Low) with a seismograph-style
  visual signal
- Which instruments (DXY, EURUSD, XAUUSD, US10Y, SPX, BTCUSD) react
  hardest, with tap-to-view definitions
- Typical release timing relative to the London/NY liquidity overlap
- "Read alongside" notes — which companion release changes how a print
  should be interpreted (e.g. NFP + wage growth)
- Compare mode — select 2–3 events and view their matrices side by side
- Deep links to a specific event (`#cpi-core-cpi`) for bookmarking

Desktop gets a two-pane layout (sticky category sidebar + list rows,
hover previews, full keyboard navigation: `/` to search, arrow keys to
move between cards, Enter to open, Esc to close). Mobile gets a card
grid and a bottom-sheet panel with swipe-to-dismiss.

**Calendar** — a full-year 2026 release schedule, organized by month
(with weekly sub-grouping) and auto-jumping to the current month on
open. Every row shows the release date, ET time, and your local-timezone
equivalent. Dates come from two sources:
- **Hardcoded, verified official dates** for indicators with a published
  yearly schedule (BLS, BEA, Census Bureau, the Fed)
- **Computed rules** for indicators that follow a fixed but unpublished
  convention (e.g. ISM Manufacturing = first business day of the month,
  UMich Sentiment = 2nd/4th Friday) — these recompute automatically and
  never go stale
- **Weekly Initial Jobless Claims** generated for every Thursday of the
  year

Fed speeches/testimony and NAR housing data (Existing/Pending Home
Sales, NAHB) don't have a fixed public schedule far in advance, so
they stay in the Reference tab without a calendar date — shown live
instead, if connected (see below).

## Going live (optional)

The calendar works fully offline with the static 2026 schedule above.
Connect a small Cloudflare Worker to layer in:
- **FRED (St. Louis Fed)** — confirms/refreshes release dates
  automatically instead of a yearly manual edit. Free forever, official
  US government data, no paywall.
- **Fed RSS feeds** — upcoming speeches & testimony
  (`speeches_and_testimony.xml`) and live confirmation of Beige Book /
  FOMC statements / Minutes the moment they post (`press_monetary.xml`).

If the worker is unreachable, everything silently falls back to the
static schedule — nothing breaks.

## What it isn't

No live price data, no forecasts/actuals feed, no backend beyond the
optional worker above. Market reactions described here are typical,
historically consistent patterns — not a guarantee of any single
release's outcome.

## Usage

Open `tremor-reference.html` directly in a browser, or host it via
GitHub Pages for a shareable link and "Add to Home Screen" support on
mobile.

To go live: see the setup comments at the top of `tremor-live-worker.js`.
