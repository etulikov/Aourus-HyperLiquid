# Git

## Commits

- **One commit per semantically complete task.** Once a task is done and verified, commit it immediately - do not wait for the end of the session and do not ask for permission.
- Never mix unrelated tasks in one commit. Two separate pieces of work mean two commits.
- Never leave finished work uncommitted. By the end of a reply the working tree is clean, apart from what is deliberately still in progress.
- Never commit unfinished or broken work. "Semantically complete" means the result stands on its own: links resolve, tests pass, the structure is consistent.

## Pushing

- **`git push` only on explicit request.** Never push on your own initiative - not when the commit is obviously ready, not right after committing, not when the push looks harmless.
- Permission to push once does not carry over to the next push: every push needs its own explicit request.
- The same applies to anything that leaves the machine: pull requests, releases, remote tags, GitHub comments.

## Commit messages

- Conventional Commits: `type(scope): description`.
- `type`: `feat`, `fix`, `docs`, `refactor`, `chore`, `test`.
- `scope`: the area touched, for example `library`, `1-signals`, `rules`.
- Description in the imperative mood, lower case, no trailing period.
- Use the body to explain what and why when the subject line does not make it obvious.
- Trailers at the end of every commit:

  ```
  Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>
  Claude-Session: <session link>
  ```

## Branches

- Work happens on `main`. Create a branch only when asked to.
