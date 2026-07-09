<!-- markdownlint-disable -->

# Hardening Report: stefanzweifel--git-auto-commit-action/v4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **stefanzweifel--git-auto-commit-action/v4** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All workflow files use mutable tag or version references instead of pinned 40-character SHA commit digests, making them vulnerable to supply-chain attacks if the referenced action is compromised or the tag is moved. Failing references include: git-auto-commit.yml: actions/checkout@v3, ./; linter.yml: actions/checkout@v3, github/super-linter@v4; release-drafter.yml: release-drafter/release-drafter@v5; tests.yml: actions/checkout@v3; update-changelog.yaml: actions/checkout@v3, stefanzweifel/changelog-updater-action@v1, stefanzweifel/git-auto-commit-action@v4; versioning.yml: Actions-R-Us/actions-tagger@latest.

Locations:

- `.github/workflows/git-auto-commit.yml:13`
- `.github/workflows/linter.yml:11`
- `.github/workflows/linter.yml:14`
- `.github/workflows/release-drafter.yml:9`
- `.github/workflows/tests.yml:11`
- `.github/workflows/update-changelog.yaml:13`
- `.github/workflows/update-changelog.yaml:17`
- `.github/workflows/update-changelog.yaml:22`
- `.github/workflows/versioning.yml:9`

### missing-permissions (severity: medium)

None of the workflow files define a top-level 'permissions:' key, and no individual jobs define job-level permissions either. Without explicit permissions, workflows run with the default (often write-all) token permissions, granting broader access than necessary.

Locations:

- `.github/workflows/git-auto-commit.yml:1`
- `.github/workflows/linter.yml:1`
- `.github/workflows/release-drafter.yml:1`
- `.github/workflows/tests.yml:1`
- `.github/workflows/update-changelog.yaml:1`
- `.github/workflows/versioning.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 9 unpinned action references across 6 workflow files by replacing mutable tag/branch references with full 40-character SHA commit digests (preserving original tags as comments). Added minimal top-level permissions blocks to all 6 workflow files: git-auto-commit.yml (contents: write), linter.yml (contents: read, statuses: write), release-drafter.yml (contents: write, pull-requests: read), tests.yml (contents: read), update-changelog.yaml (contents: write), versioning.yml (contents: write). The local action reference (./) in git-auto-commit.yml was left as-is since it refers to the local repository and does not need SHA pinning.

