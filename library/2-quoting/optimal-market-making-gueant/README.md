# Claude-agent Markdown package

This folder is a structured conversion of **Optimal market making** by Olivier Guéant (arXiv:1605.01862v5, 6 May 2017).

## What the paper gives

Two objective functions had been used for the market-making problem and were treated as different models: CARA utility of terminal mark-to-market wealth (Model A) and expected wealth minus a running inventory penalty (Model B). The paper shows their Hamilton-Jacobi-Bellman equations reduce to the same family of ODE systems, separated only by a parameter `\xi` that measures aversion to non-execution risk, and it does so for general intensity functions rather than only the exponential one. Existence, uniqueness and a verification theorem follow for the unified system.

From there it derives the generalized Guéant-Lehalle-Fernandez-Tapia formulas: closed-form approximations for the bid quote, the ask quote, the resulting spread and the skew, accurate for small inventories and visibly less so for large ones. The model is then extended to several correlated assets, where the quote on one asset depends on the inventory held in the others - the practical content of the multi-asset section is that correlation, not just own-inventory, drives the skew.

Section 6 calibrates the whole thing on two credit indices, CDX.NA.IG and CDX.NA.HY, and reports that the asymptotic quote regime is reached well inside the two-hour horizon.

## Files

- `document.md` - the paper itself, transcribed: every section, paragraph, lemma, theorem and proof of the source, all 51 numbered equations as LaTeX, all 27 footnotes, the reference list, and the figures in place.
- `equations.md` - the numbered structural equations in normalized LaTeX, including the single- and multi-asset quote formulas.
- `tables.md` - the calibrated CDX parameters of the numerical application.
- `figures.json` - figure number -> source page -> asset mapping.
- `assets/*.png` - the paper's 19 figures, cropped from source pages 32-41.
- `source_pages/*.png` - rendered images of the six source pages carrying the densest proof algebra, kept as a check on the transcription.
- `metadata.json` - machine-readable document/asset manifest, including a SHA-256 of the source PDF.

The paper has no data tables beyond the calibration, so there is no `tables/` directory.

## How faithful the transcription is

`document.md` is a transcription, not a summary. It keeps the author's own first person ("we propose", "we show"), the section titles and numbering as printed, the citation numbers in the text, and the footnotes. Where the source has a typo it keeps the typo. The mathematics was re-keyed as LaTeX and checked against 150 dpi renders of the source pages, including the long Itô verification identities (3.15) and (3.17), which are transcribed rather than left as pictures.

Two places where the source itself is ambiguous are marked rather than silently resolved. The multi-asset PDE (5.17) is reproduced with the sign layout as printed, followed by a note explaining why the placement of the $\Delta^i{H_\xi^i}'(0)$ term matters for an implementation. The parameter table of Section 6 prints $\rho=0.9$ in a cell spanning both columns, which a Markdown table cannot do; the note in the row says so.

The six source pages carrying the densest proof algebra are kept under `source_pages/` as a check on the transcription - read them when a step is disputed. The package does not carry the source PDF or a render of all 43 pages: the arXiv id and the `source_sha256` in `metadata.json` identify the exact file, so the original is one download away.

## Suggested Claude ingestion

`document.md` is the paper and answers most questions on its own. `equations.md` is the faster path when the task is to implement quotes, and `tables.md` gives realistic parameter magnitudes. Open `source_pages/` only when a specific proof step is disputed.
