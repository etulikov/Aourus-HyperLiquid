# Workflow

## Starting a task

1. Read `CLAUDE.md` and `AGENTS.md` first, together with every rule file they include. Do this before any other reading, on every task.
2. Agree on the task itself. State what you understand the problem to be and ask what is unclear, before looking for material to solve it.
3. Only then open [`library/README.md`](../../library/README.md) - the index, not the papers - and name the works that bear on the task, saying what each one contributes.
4. Open a package only after it has been named as relevant and the choice has been accepted.

## The library

- **`library/` is the repository's most important source of knowledge.** Decisions about signals, quoting, inventory risk, validation and venue mechanics are grounded in the papers collected there rather than improvised, and the model in the code should be traceable to a paper in the library.
- **Never read the whole library to solve a task.** It is meant to hold hundreds of works. Reading them all would exhaust the context budget and drown the one result that matters in two dozen that do not; more reading here makes the answer worse, not better.
- The index in `library/README.md` carries a one-line description per paper for exactly this reason: relevance is judged from the index, and a package is opened only once it has been shown to be relevant.
- Inside a package, read in order of need: `document.md` first, `equations.md` and `tables/` when the task calls for formulas or numbers, the proof appendix only when a particular step is genuinely in question.
- If the library holds nothing relevant, say so plainly instead of stretching a paper to fit.

## Nothing is changed before it is agreed

- **Do not write code.** Propose the relevant works and the approach, then stop and wait.
- **Ask before changing documentation or rules** - `AGENTS.md`, the files under `.ai/rules/`, any README, the library index. Say what you want to change and why you want to change it, and wait for an answer. Housekeeping that looks obviously right is still asked for first: the wording of these files is a decision, not a detail.
- Implementation starts on an explicit instruction to start, and not before. An approach that looks obviously right is not an instruction.
- Permission covers the task that was agreed. The next task is discussed again from the beginning.
- The gate is on writing, not on reading: searching the repository, reading code and reading the library are always allowed, and are how the proposal gets made.
