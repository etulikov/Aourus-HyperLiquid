# Claude-agent Markdown package

This folder is a structured conversion of **Dealing with the Inventory Risk: A solution to the market making problem** by Olivier Guéant, Charles-Albert Lehalle and Joaquin Fernandez-Tapia (this draft: July 2012, arXiv:1105.3115v5).

## What the paper gives

The Avellaneda-Stoikov problem again, this time with an inventory limit and a proof. A change of variables turns the Hamilton-Jacobi-Bellman equation into a system of linear ODEs, so the optimal quotes come out of a matrix exponential instead of a numerical PDE solve, and a verification theorem establishes that the quotes are in fact optimal - which, the authors note, was not available for the unconstrained problem at the time.

The paper then characterizes how the quotes behave far from the terminal time, where they settle into an asymptotic regime, and gives closed-form spectral approximations to that regime. Two extensions follow, a drift in the reference price and market impact / adverse selection, and the comparative statics are worked out in volatility, drift, intensity scale, risk aversion, intensity decay and the impact parameter. It closes with a one-day backtest on France Telecom against a naive market maker that simply posts at the first limit on each side.

## Files

- `document.md` - main reading document: section hierarchy, cleaned prose, LaTeX equations, references and relative image references.
- `equations.md` - flat index of the model and quote formulas, for retrieval and for writing code from, rather than for reading.
- `appendix-proofs.md` - the proof appendix of the paper, source pages 25-36.
- `figures.json` - figure number -> source page -> asset mapping.
- `assets/*.png` - the paper's 13 figures, plus rendered images of proof pages 25-36 under `assets/proof-pages/`.
- `metadata.json` - machine-readable document/asset manifest, including the source page of each figure and a SHA-256 of the source PDF.

The paper has no data tables, so there is no `tables/` directory.

## What the conversion normalizes, and what it leaves alone

The main paper is normalized. Hyphenation across line breaks, running headers and page numbers are gone, and the equations are transcribed into standard LaTeX keeping the paper's own symbols. The tridiagonal matrices printed in the PDF are given componentwise, by their diagonal and off-diagonal entries: this is mathematically the same object and is what an implementation actually needs.

The proof appendix is deliberately not normalized. Its algebra is dense enough that an automatic reconstruction would be a guess, so `appendix-proofs.md` keeps the fixed-width text extracted from the PDF and puts the rendered source page next to it. When an intermediate step matters, read it off the image rather than trusting the text layer.

The backtest section is kept conservative. The paper illustrates the model on a single day of France Telecom data and explicitly does not disclose the algorithm that was in production; the conversion does not fill that gap.

## Suggested Claude ingestion

Use `document.md` as the primary context file and keep `assets/` next to it so the relative image paths resolve. Pull in `equations.md` when the task is to implement the quotes, and `appendix-proofs.md` only when a proof step is actually in question - it is long and mostly raw.
