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
| [`2-quoting/`](2-quoting/) | How to turn a signal into bid/ask: spread, inventory, placement | 3 |
| [`3-risk/`](3-risk/) | Inventory risk, drawdown, tails, leverage, liquidation | - |
| [`4-validation/`](4-validation/) | Overfitting, non-stationarity, honest cost estimates | - |
| [`5-venue/`](5-venue/) | Hyperliquid specifics: perps, funding, liquidations, feeds, latency | - |

Within a category each paper is a self-contained package `<slug>/`:

```
library/<category>/<slug>/
├── document.md     - the paper itself: headings, cleaned prose, LaTeX equations, relative asset links
├── metadata.json   - machine-readable manifest (authors, date, source, tags, assets, tables)
├── README.md       - what the paper gives, what the package holds, and where the conversion leaves the source alone
├── assets/*.png    - figures, diagrams and table previews extracted from the PDF
└── tables/*.csv    - tables in machine-readable form (plus `tables.md`, the same tables as Markdown)
```

Not every paper has `assets/` or `tables/` - only those whose source has something to extract.
A paper's tags live in a `**Tags: ...**` line in the header of `document.md` and are mirrored in `metadata.json`.

The library is meant to grow to hundreds of papers, so the text about a paper is split by how expensive it is to read. This file holds one line per paper - what the work lets you compute or decide - and nothing more; it is meant to be read in full, every time. The package README holds a paragraph or two on what the paper actually says, read once a paper looks relevant. `document.md` is the paper, read once it has been chosen. A summary never lives in two places at once.
Each paper sits in exactly one category, the one it is read for; neighbouring topics are found through tags rather than duplicated folders.

## Contents

Each row says what the work lets you compute or decide. The paper's own summary lives in its package README; the paper itself in `document.md`.

### 1-signals

| Paper | Year | Authors | What it gives | Tags |
| --- | --- | --- | --- | --- |
| [The price impact of order book events](1-signals/price-impact-ob-events-cont-kukanov-stoikov/) | 2011 | Cont, Kukanov, Stoikov | Short-horizon price change is linear in order flow imbalance at the best quotes, with a slope inversely proportional to depth | PUBLIC-HL, L2, TRADES |
| [The Micro-Price](1-signals/microprice-stoikov/) | 2018 | Stoikov | Fair value as a mid-price adjustment driven by spread and best-level imbalance; estimated as a finite Markov chain | PUBLIC-HL, L2, BBO, SHORT-ALPHA |

### 2-quoting

| Paper | Year | Authors | What it gives | Tags |
| --- | --- | --- | --- | --- |
| [High-frequency trading in a limit order book](2-quoting/hft-limit-ob-avellaneda-stoikov/) | 2006 | Avellaneda, Stoikov | Optimal quotes as an inventory-dependent reservation price plus a spread, from volatility, risk aversion and order arrival intensity | EXEC, MARKET-MAKING |
| [Dealing with the Inventory Risk](2-quoting/inventory-risk-gueant-lehalle-fernandez-tapia/) | 2012 | Guéant, Lehalle, Fernandez-Tapia | The same quotes under an inventory limit, reduced to linear ODEs, with closed-form approximations, drift and market impact | EXEC, MARKET-MAKING, RISK |
| [Optimal market making](2-quoting/optimal-market-making-gueant/) | 2017 | Guéant | CARA utility and running inventory penalty unified into one ODE family; generalized GLFT closed-form quotes; several correlated assets | EXEC, MARKET-MAKING, RISK |

### 3-risk, 4-validation, 5-venue

Empty for now - see the README inside each category.
