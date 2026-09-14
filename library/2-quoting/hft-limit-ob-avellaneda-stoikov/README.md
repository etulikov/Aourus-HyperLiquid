# Claude-agent Markdown package

This folder is a structured conversion of **High-frequency trading in a limit order book** by Marco Avellaneda and Sasha Stoikov (October 5, 2006).

## Files

- `document.md` - main reading document with headings, cleaned prose, LaTeX equations and relative image references.
- `assets/*.png` - the paper's four figures, cropped from 300 dpi page renders.
- `metadata.json` - machine-readable document/asset manifest, including the source page of each figure.

The paper's three simulation tables are Markdown tables inside `document.md`; there are no CSV tables for this work.

## Suggested Claude ingestion

Use `document.md` as the primary context file and keep `assets/` next to it so the relative image paths resolve. Equation numbers such as `\tag{3.18}` are the source equation identifiers. The conversion is source-faithful rather than mathematically normalized - apparent inconsistencies in the source (for example the sign before the variance term in the Appendix value function) are preserved, not silently corrected.
