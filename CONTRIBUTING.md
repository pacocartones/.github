# Contributing

This is the default contributing guide for repositories owned by [@pacocartones](https://github.com/pacocartones) that do not have their own. When a repository has its own README, `docs/` or `AGENTS.md` with build and test instructions, those take precedence.

## Before you start

- For anything larger than a small fix, open an issue first so the approach can be agreed before you write code.
- Keep each pull request to one change. Small pull requests are reviewed faster.

## Making a change

1. Fork the repository (or create a branch, if you have write access).
2. Name the branch `<type>/<short-slug>`, where type is one of `feat`, `fix`, `docs`, `data`, `test`, `ci`, `chore`, `refactor`, using lowercase letters, digits and hyphens, for example `fix/broken-link`. Branches in forks are not checked.
3. Install with `npm ci` and run the checks the repository defines, usually `npm test` and `npm run check`.
4. Open a pull request, fill in the template, and say how you tested the change.

## Commits

- Write clear commit messages that say what changed and why.
- You may use AI tools; you are responsible for reading, understanding and testing everything you submit.

## Code of conduct

Taking part means following the [Code of Conduct](https://github.com/pacocartones/.github/blob/main/CODE_OF_CONDUCT.md).
