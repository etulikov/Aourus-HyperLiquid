# Claude-agent Markdown package

This folder is a structured conversion of **The price impact of order book events** by Rama Cont, Arseniy Kukanov and Sasha Stoikov (arXiv:1011.6402v3, March 2011).

## What the paper gives

Over short intervals prices are driven by order flow imbalance at the best quotes rather than by trade volume. OFI counts the size added to the bid and removed from the ask, so it sees limit orders and cancellations, not only trades. The relation between OFI and the price change over an interval is linear, and its slope is inversely proportional to market depth: the same imbalance moves a thin book further than a deep one.

The result is estimated on NYSE TAQ data for 50 US stocks and holds up under the usual objections - it survives intraday seasonality, it is stable across time scales from a few seconds to several minutes, and the coefficients are comparable across stocks once depth is accounted for. A scaling argument then recovers the empirical square-root law relating price impact to traded volume, which the paper presents as a consequence of the linear OFI relation rather than a separate fact.

## Files

- `document.md` - main reading document with headings, cleaned prose, LaTeX equations and relative image references.
- `tables.md` - all empirical tables rendered as Markdown tables.
- `tables/*.csv` - machine-friendly CSV versions of the paper's tables.
- `assets/*.png` - figures, diagrams and table previews extracted from the PDF.
- `metadata.json` - machine-readable document/asset manifest.

## Suggested Claude ingestion

Upload the whole folder (or ZIP). Use `document.md` as the primary context file. Keep `tables.md`/CSV files available for quantitative questions and `assets/` for visual interpretation.

All image paths are relative, e.g. `![...](assets/figure-02-ofi-scatter.png)`, and equations use standard `$...$` / `$$...$$` LaTeX syntax.
