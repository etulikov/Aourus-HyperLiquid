# Claude-agent Markdown package

This folder is a structured conversion of **Dealing with the Inventory Risk: A solution to the market making problem** by Olivier Guéant, Charles-Albert Lehalle and Joaquin Fernandez-Tapia (this draft: July 2012, arXiv:1105.3115v5).

## What the paper gives

The Avellaneda-Stoikov problem again, this time with an inventory limit and a proof. A change of variables turns the Hamilton-Jacobi-Bellman equation into a system of linear ODEs, so the optimal quotes come out of a matrix exponential instead of a numerical PDE solve, and a verification theorem establishes that the quotes are in fact optimal - which, the authors note, was not available for the unconstrained problem at the time.

The paper then characterizes how the quotes behave far from the terminal time, where they settle into an asymptotic regime, and gives closed-form spectral approximations to that regime. Two extensions follow, a drift in the reference price and market impact / adverse selection, and the comparative statics are worked out in volatility, drift, intensity scale, risk aversion, intensity decay and the impact parameter. It closes with a one-day backtest on France Telecom against a naive market maker that simply posts at the first limit on each side.

## Files

- `document.md` - the paper itself, transcribed: every section, paragraph, proposition, theorem and proof - the appendix included - with the equations as LaTeX, all 13 footnotes, the reference list, and the figures in place.
- `equations.md` - flat index of the model and quote formulas, for retrieval and for writing code from, rather than for reading.
- `figures.json` - figure number -> source page -> asset mapping.
- `assets/*.png` - the paper's 13 figures, plus rendered images of source pages 25-36 under `assets/proof-pages/`, kept as a check on the transcribed appendix.
- `metadata.json` - machine-readable document/asset manifest, including the source page of each figure and a SHA-256 of the source PDF.

The paper has no data tables, so there is no `tables/` directory.

## How faithful the transcription is

`document.md` is a transcription, not a summary. It keeps the authors' own first person ("we consider", "we show"), the section titles and numbering as printed, the citation numbers in the text, and the footnotes. Hyphenation across line breaks, running headers and page numbers are removed; nothing else is.

The proof appendix, source pages 25-36, is transcribed in full rather than left as page images - the earlier conversion kept it as fixed-width text on the grounds that re-keying would be a guess, but every step was checked here against 150 dpi renders. The tridiagonal matrices are written out as matrices, as printed. The rendered source pages stay under `assets/proof-pages/` so a disputed step can be read off the original.

The backtest section is the paper's own: it illustrates the model on a single day of France Telecom data and says explicitly that the production algorithm is not disclosed.

## Suggested Claude ingestion

Use `document.md` as the primary context file and keep `assets/` next to it so the relative image paths resolve. Pull in `equations.md` when the task is to implement the quotes - it is the same mathematics as a flat index. Open `assets/proof-pages/` only when a proof step in the appendix is actually in question.
