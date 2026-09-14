# Claude-agent Markdown package

This folder is a structured conversion of **High-frequency trading in a limit order book** by Marco Avellaneda and Sasha Stoikov (October 5, 2006).

## What the paper gives

Optimal bid and ask quotes for a dealer who faces inventory risk. The mid-price is a Brownian motion, market orders arrive as a Poisson process whose intensity decays with the distance of the quote from the mid, and the dealer maximizes exponential utility of terminal wealth over a finite horizon.

The solution separates into two steps that are worth keeping distinct in an implementation. First the dealer computes an indifference (reservation) price given the current inventory, which is the mid-price skewed against the position held. Then the quotes are placed around that price at a distance calibrated to the order book, from the probability that a quote at that distance is hit. Simulated against a naive strategy that quotes symmetrically around the mid, the inventory-based strategy gives markedly lower variance of both P&L and final inventory, at a small cost in mean P&L.

## Files

- `document.md` - main reading document with headings, cleaned prose, LaTeX equations and relative image references.
- `assets/*.png` - the paper's four figures, cropped from 300 dpi page renders.
- `metadata.json` - machine-readable document/asset manifest, including the source page of each figure.

The paper's three simulation tables are Markdown tables inside `document.md`; there are no CSV tables for this work.

## Suggested Claude ingestion

Use `document.md` as the primary context file and keep `assets/` next to it so the relative image paths resolve. Equation numbers such as `\tag{3.18}` are the source equation identifiers. The conversion is source-faithful rather than mathematically normalized - apparent inconsistencies in the source (for example the sign before the variance term in the Appendix value function) are preserved, not silently corrected.
