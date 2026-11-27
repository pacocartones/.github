# .github

Default community health files and reusable GitHub Actions workflows for [@pacocartones](https://github.com/pacocartones)' repositories. One change here reaches every repository that uses them.

- [Community health files](#community-health-files)
- [Reusable workflows](#reusable-workflows): [verify](#verify), [commit-policy](#commit-policy), [codeql](#codeql), [labels-sync](#labels-sync)
- [Pinning by SHA](#pinning-by-sha)
- [Security rules](#security-rules)
- [Developing this repository](#developing-this-repository)

## Community health files

GitHub uses these files in every repository owned by @pacocartones, private ones included, that has no file of the same kind of its own (in its root, `.github/` or `docs/`); this repository itself must stay public. A repository's own file always wins ([GitHub Docs](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)). They are the adopted files of the shared standard (standards v2 in pacocartones/dasousa-contributors-strategy); sources and licences are in [`THIRD_PARTY.md`](THIRD_PARTY.md).

| File | Purpose |
|---|---|
| [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) | Contributor Covenant 3.0, unmodified except the contact. Repositories never keep their own copy. |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Generic contribution guide. Links to [`AI_POLICY.md`](AI_POLICY.md), which is kept here for that link (it is not a community health file). |
| [`SECURITY.md`](SECURITY.md) | Report vulnerabilities privately through GitHub private vulnerability reporting. |
| [`SUPPORT.md`](SUPPORT.md) | Where to ask questions and report bugs. |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE/) | One form per issue type (Bug, Feature, Docs, Data, Task), each setting `type:` and no labels, plus `config.yml` with the support and security links. |
| [`.github/pull_request_template.md`](.github/pull_request_template.md) | What changed, why, how it was tested. |

Notes:

- Issue templates are all-or-nothing: if a repository has any file in its own `.github/ISSUE_TEMPLATE/`, none of these defaults is used there.
- The forms set the account's issue type with `type:` and apply no labels. The label set is [`.github/labels.tsv`](.github/labels.tsv) (labels v2): if a form ever applies a label, it must exist here and in every repository that uses the form.
- Inherited files are not in clones: agents read them here.
- `SECURITY.md` relies on private vulnerability reporting, which is enabled per repository (Settings → Code security).
- A license cannot be inherited; every repository needs its own `LICENSE`.

## Reusable workflows

Each workflow runs on `workflow_call` only, grants nothing at the top (`permissions: {}`), declares the narrowest permissions per job, pins every action by full commit SHA, checks out with `persist-credentials: false`, and needs no secrets. A called workflow can never get more permissions than the calling job grants, so each example below grants exactly what the workflow needs.

In the examples, replace `<sha>` with a full commit SHA of this repository (see [Pinning by SHA](#pinning-by-sha)).

### verify

[`.github/workflows/verify.yml`](.github/workflows/verify.yml): sets up Node from `.nvmrc`, runs `npm ci --ignore-scripts`, then `npm test` and `npm run check` when `package.json` defines them, then any extra commands.

| Input | Default | Description |
|---|---|---|
| `working-directory` | `.` | Directory with `package.json` and `package-lock.json`. |
| `node-version-file` | `.nvmrc` | File that pins the Node version, relative to the repository root. |
| `extra-commands` | `''` | Shell commands run last in `working-directory` (bash, stops at the first error). |

Permissions: `contents: read`.

```yaml
# .github/workflows/verify.yml in the calling repository
name: Verify
on:
  pull_request:
  push:
    branches: [main]
permissions: {}
jobs:
  verify:
    permissions:
      contents: read
    uses: pacocartones/.github/.github/workflows/verify.yml@<sha> # main 2026-11-26
    with:
      extra-commands: |
        npm run lint
        npm run build
```

### commit-policy

[`.github/workflows/commit-policy.yml`](.github/workflows/commit-policy.yml): for `pull_request` events, checks only the new commits of the pull request (base..head):

1. A commit whose author or committer looks like the maintainer (the maintainer name or login, or the login's noreply address) must use exactly the maintainer name and email.
2. Such a commit carries no AI co-author trailer (`Co-authored-by: Claude …`, `Copilot`, `Codex`, …) and no "Generated with/by …" footer. Other contributors keep their own identities and attribution choices.
3. A pull request from a branch of the repository itself uses a branch name matching `branch-pattern`. The default is the standards v2 rule: `<type>/<short-slug>` in lowercase `a-z`, `0-9` and hyphens, with dots only in a `vX.Y.Z` segment (`docs/pin-action-v1.8.0`), or `release/vX.Y.Z` for the pull request that prepares that release. Branches in forks are not checked; Dependabot's `dependabot/*` branches are exempt.

Outside a pull request it does nothing and passes.

| Input | Default | Description |
|---|---|---|
| `maintainer-name` | `Paco Cartones` | The maintainer's `git user.name`. |
| `maintainer-email` | `253313177+pacocartones@users.noreply.github.com` | The maintainer's `git user.email`. |
| `maintainer-login` | `pacocartones` | The maintainer's GitHub login. |
| `branch-pattern` | `^((feat\|fix\|docs\|data\|test\|ci\|chore\|refactor)/((([a-z0-9]*\|v[0-9]+\.[0-9]+\.[0-9]+)-)+([a-z0-9]*\|v[0-9]+\.[0-9]+\.[0-9]+)\|[a-z0-9]+\|v[0-9]+\.[0-9]+\.[0-9]+)\|release/v[0-9]+\.[0-9]+\.[0-9]+)$` | Extended regex for branch names (standards v2, see rule 3). |

Permissions: `contents: read`.

```yaml
# .github/workflows/commit-policy.yml in the calling repository
name: Commit policy
on:
  pull_request:
permissions: {}
jobs:
  commits:
    permissions:
      contents: read
    uses: pacocartones/.github/.github/workflows/commit-policy.yml@<sha> # main 2026-11-26
```

The `uses:` line lives in the pull request's own tree, so a pull request could point it elsewhere. Make the check required in branch protection and review changes to workflow files.

### codeql

[`.github/workflows/codeql.yml`](.github/workflows/codeql.yml): CodeQL code scanning for one language.

| Input | Default | Description |
|---|---|---|
| `language` | `javascript-typescript` | CodeQL language (`python`, `actions`, …). |
| `build-mode` | `none` | `none`, `autobuild` or `manual`. |

Permissions: `security-events: write`, `actions: read`, `contents: read`.

```yaml
# .github/workflows/codeql.yml in the calling repository
name: CodeQL
on:
  pull_request:
  schedule:
    - cron: '0 4 * * 1'
  workflow_dispatch: {}
permissions: {}
jobs:
  analyze:
    permissions:
      security-events: write
      actions: read
      contents: read
    uses: pacocartones/.github/.github/workflows/codeql.yml@<sha> # main 2026-11-26
```

For several languages, add `strategy: { matrix: { language: [javascript-typescript, actions] } }` to the job and pass `with: { language: '${{ matrix.language }}' }`.

### labels-sync

[`.github/workflows/labels-sync.yml`](.github/workflows/labels-sync.yml): creates or updates the calling repository's labels from a TSV file. Run it by hand from a `workflow_dispatch` workflow.

| Input | Default | Description |
|---|---|---|
| `labels-file` | `.github/labels.tsv` | The labels file. |
| `prune` | `false` | Delete labels that are not in the file (they are also removed from issues and pull requests). |

Permissions: `contents: read`, `issues: write`.

File format: one label per line, tab-separated `name`, `color` (six hex digits, no `#`) and `description` (may be empty). Blank lines and lines starting with `#` are ignored.

```tsv
# name	color	description (labels v2: see .github/labels.tsv)
needs info	fbca04	Waiting for more information from the author
good first issue	7057ff	Good for newcomers
```

```yaml
# .github/workflows/labels-sync.yml in the calling repository
name: Labels sync
on:
  workflow_dispatch:
    inputs:
      prune:
        description: Delete labels that are not in .github/labels.tsv
        type: boolean
        default: false
permissions: {}
jobs:
  sync:
    permissions:
      contents: read
      issues: write
    uses: pacocartones/.github/.github/workflows/labels-sync.yml@<sha> # main 2026-11-26
    with:
      prune: ${{ inputs.prune }}
```

## Pinning by SHA

Pin each reusable workflow to a full 40-character commit SHA of this repository, with the branch and date as a comment. A SHA cannot move, so a later change here (or a compromised branch) never reaches a caller until the caller updates the pin on purpose.

```bash
git ls-remote https://github.com/pacocartones/.github refs/heads/main
```

Copy the SHA it prints into `uses: pacocartones/.github/.github/workflows/<file>.yml@<sha> # main YYYY-MM-DD`. To take a change, update the SHA in a pull request and let CI run on it. `@main` also works but runs whatever is on `main` at the time, so use it only where that is wanted.

## Security rules

[`tests/workflow-policy.test.mjs`](tests/workflow-policy.test.mjs) enforces these on every workflow in this repository, including the next one added:

1. every action is pinned by a full commit SHA with its version as a comment;
2. `permissions: {}` at the top, and explicit permissions on every job;
3. every `actions/checkout` sets `persist-credentials: false`;
4. no `pull_request_target` or `workflow_run` triggers;
5. text an outsider controls (titles, bodies, branch names) never appears in a `run:` script;
6. the reusable workflows are `workflow_call` only and read no secrets.

## Releases

This repository has no releases, tags or CHANGELOG: callers pin its reusable workflows by full commit SHA (see [Pinning by SHA](#pinning-by-sha)). Maintainers and governance: [MAINTAINERS.md](MAINTAINERS.md), [GOVERNANCE.md](GOVERNANCE.md).

## Developing this repository

[`ci.yml`](.github/workflows/ci.yml) runs on every pull request and push to `main`: [actionlint](https://github.com/rhysd/actionlint) (with shellcheck) on every workflow, the tests through the local `verify.yml`, and the local `commit-policy.yml`.

```bash
npm test
```

[`tests/commit-policy.test.mjs`](tests/commit-policy.test.mjs) runs the script embedded in `commit-policy.yml` exactly as written there, against throwaway git repositories. To lint locally:

```bash
go install github.com/rhysd/actionlint/cmd/actionlint@v1.7.12
```

```bash
actionlint
```
