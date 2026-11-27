# Contributing

*Structure based on [nayafia/contributing-template](https://github.com/nayafia/contributing-template) (commit `ab3044b`, [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/)) and the CONTRIBUTING checklist in [Open Source Guides, Starting an Open Source Project](https://opensource.guide/starting-a-project/) ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)). Modified: the template's prompts and quoted examples from other projects are replaced by our own text.*

## Introduction

Thank you for taking the time to help. This guide applies to every repository of @pacocartones that has no CONTRIBUTING file of its own. Fixes, tests, documentation and well-reported bugs are all welcome.

## Ground Rules

- Follow the [Code of Conduct](CODE_OF_CONDUCT.md).
- AI assistance is allowed under the [AI policy](AI_POLICY.md). You answer for every line you submit.
- One change per pull request, with the repository's checks passing.
- No CLA and no sign-off are required.

## Your First Contribution

Issues labelled `good first issue` are small and scoped for people new to the project; they are kept for humans, not agents. `help wanted` issues are larger. Comment on the issue before you start and wait for the maintainer to confirm, so two people do not do the same work.

## Getting Started

1. Fork the repository and create a branch from the latest `main`, named `type/short-description` (for example `fix/login-timeout`).
2. Make the change. If it changes behaviour, add a test that fails without it.
3. Run the checks the repository's README or CI workflows (`.github/workflows/`) list.
4. Write commit messages in [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) form (`fix: stop retrying on 404`).
5. Open a pull request and fill in its template.

Small, obvious fixes (a typo, a broken link) need no issue first.

## How to Report a Bug

If you find a security vulnerability, do not open an issue: follow [SECURITY.md](SECURITY.md).

For any other bug, open an issue with the **Bug report** form: the version, what you did, what you expected and what happened instead.

## How to Suggest a Feature or Enhancement

Open an issue with the **Feature request** form. Describe the problem first, then the solution you have in mind. The maintainer decides the scope, as [GOVERNANCE.md](GOVERNANCE.md) says.

## Code Review Process

The maintainer reviews every pull request and aims to give a first response within 3 business days, best effort. That is a target, not a promise. Nothing merges without a human review, and only the maintainer merges.

## Community

Questions go where [SUPPORT.md](SUPPORT.md) says. The people who maintain each repository are in its MAINTAINERS.md.

## Conventions

- **Commits**: Conventional Commits 1.0.0, subject in the imperative, a body that says why.
- **Issues**: each form sets the issue type (Bug, Feature, Docs, Data, Task). Labels only mark the area, the triage state and entry points such as `good first issue`.
