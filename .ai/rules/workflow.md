# Workflow

## Starting a task

- Read `CLAUDE.md` and `AGENTS.md` first, together with every rule file they include. Do this before any other reading, on every task.
- Then read [`library/README.md`](../../library/README.md) - the index, not the papers.
- From that index, name the works that bear on the task at hand and say what each one contributes. Present this before doing anything else.

## The library

- **`library/` is the repository's most important source of knowledge.** Decisions about signals, quoting, inventory risk, validation and venue mechanics are grounded in the papers collected there rather than improvised, and the model in the code should be traceable to a paper in the library.
- **Never read the whole library to solve a task.** The index exists precisely so that a package is opened only once it has been shown to be relevant. Reading everything spends the context budget and buries the result that actually matters.
- Inside a package, read in order of need: `document.md` first, `equations.md` and `tables/` when the task calls for formulas or numbers, the proof appendix only when a particular step is genuinely in question.
- If the library holds nothing relevant, say so plainly instead of stretching a paper to fit.

## Discussion before implementation

- **Do not write code.** Propose the relevant works and the approach, then stop and wait.
- The solution is settled in conversation first. Implementation starts on an explicit instruction to start, and not before - an approach that looks obviously right is not an instruction.
- Permission to implement covers the task that was agreed. The next task is discussed again from the beginning.
- The gate is on writing, not on reading: searching the repository, reading code and reading the library are always allowed, and are how the proposal gets made.
