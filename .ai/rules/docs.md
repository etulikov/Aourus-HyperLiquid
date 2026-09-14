# Documentation and comments

## Language

- **Everything written into the repository is in English.** No exceptions: Markdown documents, READMEs, rule files, code comments, docstrings, commit messages, PR descriptions, log and error strings, identifiers, test names, TODOs, JSON/YAML values meant for humans.
- This holds regardless of the language of the conversation that produced the text. Chat is not the repository.
- If you find Russian text already committed - in a file you are editing or one you are merely passing through - translate it to English as part of the work, and say so.
- Do not transliterate and do not invent a translation: use the term the literature already uses - order book, quote, spread, inventory, slippage, adverse selection, funding, leverage.
- The only non-English text allowed in the repository is a verbatim quotation of an external source, and only when the exact wording is the point; mark it as a quotation and follow it with an English gloss.

## Style

- Write for a reader who has not seen the conversation: state what a thing is and why it exists, not what was just changed.
- Prefer plain declarative sentences over bullet fragments when explaining a decision.
- Comment the non-obvious - a constraint, a trade-off, a reason. Do not narrate what the code already says.

## The paper library

- **`document.md` is a transcription of the paper, never a summary of it.** The library exists to be the source of truth; a retelling that sits where the paper should sit is worse than no paper, because nothing on its surface says it is a retelling.
- Transcription means: the author's own voice and person, the section titles and numbering as printed, the citation numbers in the text, the footnotes, the proofs. Remove only what the page format imposed - line-break hyphenation, running headers, page numbers. Keep the source's typos and its ambiguities; where an ambiguity matters for an implementation, mark it in a note rather than resolving it silently.
- Mathematics is re-keyed as LaTeX and checked against a render of the source page. A PDF text layer scrambles fractions, superscripts and matrix notation exactly where a proof is hardest to read, so the render, not the text layer, is the authority.
- The paper's summary belongs in the package `README.md`, under "What the paper gives", and its one-line form in the library index. Those are the places a reader knows to read as description.
- State the check that was actually run in `metadata.json`, so a later reader can tell a verified conversion from an assumed one.
