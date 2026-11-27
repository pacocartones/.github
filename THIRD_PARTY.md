# Third-party notices

The community files in this repository come from the shared standard (standards v2) of pacocartones/dasousa-contributors-strategy, which adopted them from the sources below. Copied from that repository unchanged: the community files at commit 6caf476, GOVERNANCE.md, MAINTAINERS.md, LICENSES/Apache-2.0.txt and the Scorecard workflow at commit 38ac8a1.

## Adopted files

These files are copied unchanged from `templates/` in pacocartones/dasousa-contributors-strategy (standards v2). Each one names its source in its first lines. Read on 2026-11-27 at the commit given; modified only where the standard's decisions require.

| File | Source and revision | Licence | Change |
|---|---|---|---|
| `CODE_OF_CONDUCT.md` | [Contributor Covenant 3.0](https://www.contributor-covenant.org/version/3/0/code_of_conduct/), `EthicalSource/contributor_covenant` `content/version/3/0/code_of_conduct.md` @ `8d00b91` | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) | Site front matter dropped; the reporting placeholder replaced by the contact, and the enforcement placeholder note removed. Its Attribution section is kept as is. |
| `SECURITY.md` | [ossf/oss-vulnerability-guide](https://github.com/ossf/oss-vulnerability-guide) `templates/security_policies/github_security_policy.md` @ `40ecfe2` | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) | E-mail replaced by GitHub private vulnerability reporting; supported-versions section and a line for private repositories added. |
| `CONTRIBUTING.md` | [nayafia/contributing-template](https://github.com/nayafia/contributing-template) `CONTRIBUTING-template.md` @ `ab3044b`; checklist from [Open Source Guides](https://opensource.guide/starting-a-project/) | CC0 1.0; CC BY 4.0 | Headings kept; prompts and the other projects' quoted examples replaced by our text. |
| `.github/pull_request_template.md` | [stevemao/github-issue-templates](https://github.com/stevemao/github-issue-templates) `checklist/PULL_REQUEST_TEMPLATE.md` @ `82f4289` | CC0 1.0 | «What and why» and «AI assistance» sections added. |
| `.github/ISSUE_TEMPLATE/bug.yml`, `.github/ISSUE_TEMPLATE/feature.yml`, `.github/ISSUE_TEMPLATE/docs.yml`, `.github/ISSUE_TEMPLATE/data.yml` | GitHub Docs issue-form examples, `github/docs` @ `df6faa2`; [vitejs/vite](https://github.com/vitejs/vite/tree/main/.github/ISSUE_TEMPLATE) `bug_report.yml`, `feature_request.yml`, `docs.yml` @ `7d0c054` | CC BY 4.0; MIT (notice below) | `type:` set to the account type, no labels, Vite-specific fields and links removed; `data.yml` reuses the docs form's structure. |
| `.github/ISSUE_TEMPLATE/task.yml`, `.github/ISSUE_TEMPLATE/config.yml` | GitHub Docs issue-form and `config.yml` examples, `github/docs` @ `df6faa2` | CC BY 4.0 | Minimal Task form; our contact links. |
| `GOVERNANCE.md`, `MAINTAINERS.md` | [cncf/project-template](https://github.com/cncf/project-template) `GOVERNANCE-maintainer.md`, `MAINTAINERS.md` @ `e66ba44` | Apache-2.0 (`LICENSES/Apache-2.0.txt`) | Trimmed for one maintainer: council, voting, meetings, CNCF resources and affiliations removed; scope column added. |
| `.github/workflows/scorecard.yml` | [ossf/scorecard-action](https://github.com/ossf/scorecard-action) `examples/scorecard.yml` @ `df56f2d` (action v2.6.0) | Apache-2.0 | Attribution header only. |
| `AI_POLICY.md`, `SUPPORT.md` | Own text; the policies and page they link to informed them. No text copied: those policies state no licence. | — | — |

Not copied, only linked: `github/.github` (no licence), the projects' AI policies (no licence), and CC BY-SA guides other than the Contributor Covenant.

### vitejs/vite

```
MIT License

Copyright (c) 2019-present, VoidZero Inc. and Vite contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
