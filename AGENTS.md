# Working in this repository

This repository holds the default community files and the reusable workflows of @pacocartones' repositories. One change here reaches every repository that uses them.

- The community files here are the adopted texts of the shared standard (standards v2 in pacocartones/dasousa-contributors-strategy, `templates/`). Change them there first, then copy them here unchanged; see [THIRD_PARTY.md](THIRD_PARTY.md).
- Agents never merge, not even their own pull request: open a draft and leave the merge to the maintainer. Maintainers are in [MAINTAINERS.md](MAINTAINERS.md).
- Every workflow: `permissions: {}` at the top and the narrowest permissions per job, actions pinned by full commit SHA with the version as a comment, `persist-credentials: false` on checkout, no `pull_request_target` with a checkout of the pull request. `npm test` checks this.
