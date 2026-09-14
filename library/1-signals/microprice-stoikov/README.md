# Claude-agent Markdown package

This folder is a structured conversion of **The Micro-Price: A High Frequency Estimator of Future Prices** by Sasha Stoikov (April 18, 2018; SSRN id3165260).

## What the paper gives

The micro-price is the limit of a sequence of expected mid-prices, and is therefore a martingale by construction: the fair price given the current state of the order book. It is written as an adjustment to the mid-price driven by two observables, the spread and the imbalance between the sizes at the best bid and best ask, and it is estimated from high-frequency data as a Markov chain on a finite state space rather than fitted as a regression.

Empirically it predicts the future price better than the mid-price or the volume-weighted mid over horizons from 10 seconds to 3 minutes. The shape of the adjustment differs sharply between large-tick and small-tick instruments - BAC and CVX are the two worked examples - which matters when the same estimator is applied across a venue with mixed tick regimes.

## Files

- `document.md` - main reading document with headings, cleaned prose, LaTeX equations and relative image references.
- `assets/*.png` - the paper's five figures, cropped from the source PDF.
- `metadata.json` - machine-readable document/asset manifest, including the source page and caption of each figure.

The paper contains no data tables.

## Suggested Claude ingestion

Use `document.md` as the primary context file and keep `assets/` next to it so the relative image paths resolve. Inline mathematics uses `$...$`, display mathematics `$$...$$`, and equation numbers from the paper are preserved with `\tag{...}` where present.

## Source-faithfulness notes

The conversion preserves the paper's notation and wording rather than silently reconciling apparent source inconsistencies. In particular:

1. Equation (4) defines `S = P^a - P^b`, while Assumption 1 later prints `S_t = 1/2(P_t^a - P_t^b)` and calls it the bid-ask spread. Both are retained as printed.
2. The prose after Theorem 2.1 says "Theorem 1 provides ..."; this is retained from the source.
3. Appendix B's displayed second-adjustment derivation is transcribed as printed, including the expectation involving `I_t - 1/2`.
4. PDF line-wrap artifacts, repeated page headers/footers, page numbers and the SSRN footer have been removed.
