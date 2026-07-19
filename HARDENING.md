<!-- markdownlint-disable -->

# Hardening Report: stefanzweifel--git-auto-commit-action/v4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **stefanzweifel--git-auto-commit-action/v4** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All workflow files use mutable tag/version refs instead of pinned 40-character SHA commit hashes, making them vulnerable to supply-chain attacks if the referenced action is compromised or the tag is moved.

- .github/workflows/git-auto-commit.yml: `actions/checkout@v3`
- .github/workflows/linter.yml: `actions/checkout@v3`, `github/super-linter@v4`
- .github/workflows/release-drafter.yml: `release-drafter/release-drafter@v5`
- .github/workflows/tests.yml: `actions/checkout@v3`
- .github/workflows/update-changelog.yaml: `actions/checkout@v3`, `stefanzweifel/changelog-updater-action@v1`, `stefanzweifel/git-auto-commit-action@v4`
- .github/workflows/versioning.yml: `Actions-R-Us/actions-tagger@latest` (especially dangerous: `@latest` is a moving target)

Locations:

- `.github/workflows/git-auto-commit.yml:13`
- `.github/workflows/linter.yml:11`
- `.github/workflows/linter.yml:14`
- `.github/workflows/release-drafter.yml:11`
- `.github/workflows/tests.yml:11`
- `.github/workflows/update-changelog.yaml:10`
- `.github/workflows/update-changelog.yaml:14`
- `.github/workflows/update-changelog.yaml:18`
- `.github/workflows/versioning.yml:9`

### missing-permissions (severity: medium)

None of the workflow files define a top-level `permissions:` key, and no individual job defines its own `permissions:` block. This means all jobs run with the default (potentially broad) token permissions granted by the repository settings, violating the principle of least privilege.

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

Fixed all 6 workflow files:

1. git-auto-commit.yml: Pinned actions/checkout@v3 → @f43a0e5ff2bd294095638e18286ca9a3d1956744; added `permissions: contents: read`.

2. linter.yml: Pinned actions/checkout@v3 → @f43a0e5ff2bd294095638e18286ca9a3d1956744 and github/super-linter@v4 → @985ef206aaca4d560cb9ee2af2b42ba44adc1d55; added `permissions: contents: read`.

3. release-drafter.yml: Pinned release-drafter/release-drafter@v5 → @09c613e259eb8d4e7c81c2cb00618eb5fc4575a7; added `permissions: contents: write, pull-requests: read` (release drafter needs to write draft releases).

4. tests.yml: Pinned actions/checkout@v3 → @f43a0e5ff2bd294095638e18286ca9a3d1956744; added `permissions: contents: read`.

5. update-changelog.yaml: Pinned actions/checkout@v3 → @f43a0e5ff2bd294095638e18286ca9a3d1956744, stefanzweifel/changelog-updater-action@v1 → @a938690fad7edf25368f37e43a1ed1b34303eb36, stefanzweifel/git-auto-commit-action@v4 → @3ea6ae190baf489ba007f7c92608f33ce20ef04a; added `permissions: contents: write` (commits to master).

6. versioning.yml: Pinned Actions-R-Us/actions-tagger@latest → @330ddfac760021349fef7ff62b372f2f691c20fb; added `permissions: contents: write` (manages tags/releases).

All original tag names preserved as inline comments for readability.

