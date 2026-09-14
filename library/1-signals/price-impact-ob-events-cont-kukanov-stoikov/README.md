# Claude-agent Markdown package

This folder is a structured conversion of **The price impact of order book events** by Rama Cont, Arseniy Kukanov and Sasha Stoikov (arXiv:1011.6402v3, March 2011).

## Files

- `document.md` - main reading document with headings, cleaned prose, LaTeX equations and relative image references.
- `tables.md` - all empirical tables rendered as Markdown tables.
- `tables/*.csv` - machine-friendly CSV versions of the paper's tables.
- `assets/*.png` - figures, diagrams and table previews extracted from the PDF.
- `metadata.json` - machine-readable document/asset manifest.

## Suggested Claude ingestion

Upload the whole folder (or ZIP). Use `document.md` as the primary context file. Keep `tables.md`/CSV files available for quantitative questions and `assets/` for visual interpretation.

All image paths are relative, e.g. `![...](assets/figure-02-ofi-scatter.png)`, and equations use standard `$...$` / `$$...$$` LaTeX syntax.
