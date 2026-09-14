# Algorithmic trading paper library

## Tags

| Tag | Meaning |
| --- | --- |
| PUBLIC-HL | Testable on the public Hyperliquid feeds: bbo / l2Book / trades / asset context. |
| CROSS | Requires public feeds from other venues (Binance/Bybit/Coinbase/CME and the like). |
| EXEC | Placement, market making, inventory, fill and adverse selection. |
| L3/L4 | Per-order / order-id data. For HL this is an optional research track, not a prerequisite. |
| PERP/FUNDING | Perpetuals mechanics: funding, basis, liquidation. |
| VALIDATION/REGIME | Defences against backtest overfitting and non-stationarity. |
| BBO | Best Bid / Best Offer. Best bid and best ask only: price, size, sometimes order count. The lightest top-of-book feed. |
| TRADES | Trade stream: price, size, aggressor side, timestamp, trade id and so on. |
| ORDER-FLOW | The stream of actions that change the market: market trades, limit adds, cancels, updates. Broader than trades alone. |
| L2 | Order book aggregated by price level, for example price -> total size, without individual order IDs. |
| MARKET-MAKING | Posting bid/ask, inventory management, spread, adverse selection, quoting. |
| HAWKES | Hawkes process models, where an event raises the probability of further events shortly after it. Commonly applied to trades/cancels/limit orders to model clustering and self-excitation. |
| SHORT-ALPHA | Short-horizon predictive signal: probability of a price move roughly 10-500 ms or a few events ahead. |
| RISK | Inventory risk, liquidation risk, drawdown, adverse selection, tail risk, leverage and so on. |
| LATENCY | Data and execution delay: who saw the event first, how long the feed takes, order ack, fill and so on. |

## Layout

Papers are grouped by their role in the trading stack: signal -> quote -> risk -> validation -> venue.

| Category | Scope | Papers |
| --- | --- | --- |
| [`1-signals/`](1-signals/) | What can be predicted from the data: fair value, short horizon, order flow impact | 2 |
| [`2-quoting/`](2-quoting/) | How to turn a signal into bid/ask: spread, inventory, placement | 2 |
| [`3-risk/`](3-risk/) | Inventory risk, drawdown, tails, leverage, liquidation | - |
| [`4-validation/`](4-validation/) | Overfitting, non-stationarity, honest cost estimates | - |
| [`5-venue/`](5-venue/) | Hyperliquid specifics: perps, funding, liquidations, feeds, latency | - |

Within a category each paper is a self-contained package `<slug>/`:

```
library/<category>/<slug>/
├── document.md     - the paper itself: headings, cleaned prose, LaTeX equations, relative asset links
├── metadata.json   - machine-readable manifest (authors, date, source, tags, assets, tables)
├── README.md       - what the package holds, its state, and where the conversion deliberately leaves the source alone
├── assets/*.png    - figures, diagrams and table previews extracted from the PDF
└── tables/*.csv    - tables in machine-readable form (plus `tables.md`, the same tables as Markdown)
```

Not every paper has `assets/` or `tables/` - only those whose source has something to extract.
A paper's tags live in a `**Tags: ...**` line in the header of `document.md` and are mirrored in `metadata.json`.
Every paper also gets a one-line "What it gives" entry in the tables below, stating what the work lets you compute or decide.
The library is meant to grow to hundreds of papers, so those two columns are what relevance is judged from: the tables are read in full, the packages are not.
Each paper sits in exactly one category, the one it is read for; neighbouring topics are found through tags rather than duplicated folders.

## Contents

### 1-signals

| Paper | Year | Authors | What it gives | Tags |
| --- | --- | --- | --- | --- |
| [The price impact of order book events](1-signals/price-impact-ob-events-cont-kukanov-stoikov/document.md) | 2011 | Cont, Kukanov, Stoikov | Short-horizon price change is linear in order flow imbalance at the best quotes, with a slope inversely proportional to depth | PUBLIC-HL, L2, TRADES |
| [The Micro-Price: A High Frequency Estimator of Future Prices](1-signals/microprice-stoikov/document.md) | 2018 | Stoikov | Fair value as a mid-price adjustment driven by spread and best-level imbalance; estimated as a finite Markov chain | PUBLIC-HL, L2, BBO, SHORT-ALPHA |

**The price impact of order book events.** Cont, Kukanov & Stoikov, March 2011 (arXiv:1011.6402v3). Using NYSE TAQ data for 50 US stocks, the paper shows that over short intervals prices are driven by order flow imbalance (OFI) at the best quotes rather than by trade volume. The relation between OFI and price change is linear, with a slope inversely proportional to market depth; it is robust to intraday seasonality and stable across time scales and across stocks. A scaling argument then recovers the empirical "square-root" law for volume.
Package: `document.md`, `tables.md`, `metadata.json`, 15 figures in `assets/`, 6 tables in `tables/`.

**The Micro-Price.** Stoikov, April 2018 (SSRN id3165260). The micro-price is the limit of a sequence of expected mid-prices, a martingale by construction and therefore the "fair" price given the state of the order book. It is expressed as an adjustment to the mid-price driven by the spread and the imbalance at the best levels, and estimated from high-frequency data as a Markov chain on a finite state space. Empirically it predicts price better than the mid-price or the weighted mid-price over horizons of 10 seconds to 3 minutes, and the adjustment behaves differently for large-tick (BAC) and small-tick (CVX) stocks.
Package: `document.md`, `metadata.json`, 5 figures in `assets/`. The paper has no data tables.

### 2-quoting

| Paper | Year | Authors | What it gives | Tags |
| --- | --- | --- | --- | --- |
| [High-frequency trading in a limit order book](2-quoting/hft-limit-ob-avellaneda-stoikov/document.md) | 2006 | Avellaneda, Stoikov | Optimal quotes as an inventory-dependent reservation price plus a spread, from volatility, risk aversion and order arrival intensity | EXEC, MARKET-MAKING |
| [Dealing with the Inventory Risk](2-quoting/inventory-risk-gueant-lehalle-fernandez-tapia/document.md) | 2012 | Guéant, Lehalle, Fernandez-Tapia | The same quotes under an inventory limit, reduced to linear ODEs, with closed-form approximations, drift and market impact | EXEC, MARKET-MAKING, RISK |

**High-frequency trading in a limit order book.** Avellaneda & Stoikov, October 2006. Optimal bid and ask quotes for a dealer facing inventory risk: the mid-price is a Brownian motion and market orders arrive as a Poisson process whose intensity decays with distance from the mid. The solution comes in two steps - an indifference price given current inventory, then calibration of the quotes to the order book. Simulations show markedly lower variance of P&L and of final inventory than symmetric quoting around the mid.
Package: `document.md`, `metadata.json`, 4 figures in `assets/`. The paper's three simulation tables are Markdown tables inside `document.md`; there are no CSV tables.

**Dealing with the Inventory Risk.** Guéant, Lehalle & Fernandez-Tapia, July 2012 (arXiv:1105.3115v5). The Avellaneda-Stoikov problem revisited, this time with an inventory limit and a proof. A change of variables turns the HJB equation into a system of linear ODEs, so the optimal quotes follow from a matrix exponential instead of a numerical PDE solve, and a verification theorem is available. The paper then works out how the quotes behave far from the horizon and gives closed-form spectral approximations, extends the model to a price drift and to market impact / adverse selection, and reads off the comparative statics in sigma, mu, A, gamma, k and the impact parameter. It closes with a one-day backtest on France Telecom against a naive market maker that simply posts at the first limit.
Package: `document.md`, `equations.md`, `appendix-proofs.md`, `figures.json`, `metadata.json`, 13 figures plus 12 rendered proof pages in `assets/`. The paper has no data tables.

### 3-risk, 4-validation, 5-venue

Empty for now - see the README inside each category.
