# Claude-agent Markdown package

This folder is a structured conversion of **Optimal market making** by Olivier Guéant (arXiv:1605.01862v5, 6 May 2017).

## What the paper gives

Two objective functions had been used for the market-making problem and were treated as different models: CARA utility of terminal mark-to-market wealth (Model A) and expected wealth minus a running inventory penalty (Model B). The paper shows their Hamilton-Jacobi-Bellman equations reduce to the same family of ODE systems, separated only by a parameter `\xi` that measures aversion to non-execution risk, and it does so for general intensity functions rather than only the exponential one. Existence, uniqueness and a verification theorem follow for the unified system.

From there it derives the generalized Guéant-Lehalle-Fernandez-Tapia formulas: closed-form approximations for the bid quote, the ask quote, the resulting spread and the skew, accurate for small inventories and visibly less so for large ones. The model is then extended to several correlated assets, where the quote on one asset depends on the inventory held in the others - the practical content of the multi-asset section is that correlation, not just own-inventory, drives the skew.

Section 6 calibrates the whole thing on two credit indices, CDX.NA.IG and CDX.NA.HY, and reports that the asymptotic quote regime is reached well inside the two-hour horizon.

## Files

- `document.md` - main reading document: section hierarchy, cleaned prose, the argument of each section, figures.
- `equations.md` - the numbered structural equations in normalized LaTeX, including the single- and multi-asset quote formulas.
- `tables.md` - the calibrated CDX parameters of the numerical application.
- `figures.json` - figure number -> source page -> asset mapping.
- `assets/*.png` - the paper's 19 figures, cropped from source pages 32-41.
- `source_pages/*.png` - rendered images of the six source pages whose proofs are not re-keyed.
- `metadata.json` - machine-readable document/asset manifest, including a SHA-256 of the source PDF.

The paper has no data tables beyond the calibration, so there is no `tables/` directory.

## What the conversion normalizes, and what it leaves alone

The structural mathematics is re-keyed as LaTeX. The long proof-only Itô and jump identities are not: a PDF text layer scrambles fractions, superscripts and matrix notation exactly where a proof is hardest to check, so those six pages are kept as images and pointed at from `equations.md`. Where the paper's own sign layout is easy to misread - the quadratic-gradient term of the multi-asset system - `equations.md` says so and sends you to the page.

The package does not carry the source PDF or a render of all 43 pages. The arXiv id and the `source_sha256` in `metadata.json` identify the exact file, so the original is one download away, and the package stays around two megabytes instead of fourteen.

## Suggested Claude ingestion

`document.md` for the argument, `equations.md` when the task is to implement quotes, `tables.md` for realistic parameter magnitudes. Open `source_pages/` only when a specific proof step is in question.
