<!-- markdownlint-disable -->

# Hardening Report: stefanzweifel--git-auto-commit-action/v7.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **stefanzweifel--git-auto-commit-action/v7.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference actions using mutable tags or branch names instead of full 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced tag is moved or the action is compromised. Failing references:
- .github/workflows/git-auto-commit.yml: `actions/checkout@v6`
- .github/workflows/linter.yml: `actions/checkout@v6`, `github/super-linter@v7`
- .github/workflows/release-drafter.yml: `release-drafter/release-drafter@v6`
- .github/workflows/tests.yml: `actions/checkout@v6`
- .github/workflows/update-changelog.yaml: `actions/checkout@v6`, `stefanzweifel/changelog-updater-action@v1`, `stefanzweifel/git-auto-commit-action@v7`
- .github/workflows/versioning.yml: `Actions-R-Us/actions-tagger@latest`

Locations:

- `.github/workflows/git-auto-commit.yml:18`
- `.github/workflows/linter.yml:10`
- `.github/workflows/linter.yml:13`
- `.github/workflows/release-drafter.yml:16`
- `.github/workflows/tests.yml:12`
- `.github/workflows/update-changelog.yaml:18`
- `.github/workflows/update-changelog.yaml:22`
- `.github/workflows/update-changelog.yaml:27`
- `.github/workflows/versioning.yml:16`

### missing-permissions (severity: medium)

Two workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any of their jobs. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions, violating the principle of least privilege.
- linter.yml: no permissions defined at top-level or job level
- tests.yml: no permissions defined at top-level or job level

Locations:

- `.github/workflows/linter.yml:1`
- `.github/workflows/tests.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Pinned all 9 unpinned action references to full commit SHAs: actions/checkout@v6 → d23441a48e516b6c34aea4fa41551a30e30af803 (used in 4 files), github/super-linter@v7 → b807e99ddd37e444d189cfd2c2ca1274d8ae8ef1, release-drafter/release-drafter@v6 → 6a93d829887aa2e0748befe2e808c66c0ec6e4c7, stefanzweifel/changelog-updater-action@v1 → a938690fad7edf25368f37e43a1ed1b34303eb36, stefanzweifel/git-auto-commit-action@v7 → 4a55954c782fc1ea30b9056cd3e7a2b40ca8887d, Actions-R-Us/actions-tagger@latest → 330ddfac760021349fef7ff62b372f2f691c20fb. Added top-level `permissions: contents: read` to linter.yml and tests.yml to fix missing-permissions findings.

