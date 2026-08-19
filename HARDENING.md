<!-- markdownlint-disable -->

# Hardening Report: michalvankodev--copy-issue-labels/v2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **michalvankodev--copy-issue-labels/v2.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses 'michalvankodev/copy-issue-labels@v1.3.0', which is a mutable tag reference rather than a pinned 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit, enabling supply-chain attacks. Pin to a full SHA, e.g. 'michalvankodev/copy-issue-labels@<40-char-sha> # v1.3.0'.

Locations:

- `.github/workflows/copy-labels.yml:8`

### missing-permissions (severity: medium)

The workflow file has no top-level 'permissions:' key and the only job ('copy-labels') also has no job-level 'permissions:' key. Without explicit permissions, the workflow inherits the repository default (often 'write' for GITHUB_TOKEN), granting broader access than necessary. Add a minimal permissions block, e.g. 'permissions: contents: read'.

Locations:

- `.github/workflows/copy-labels.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both findings in .github/workflows/copy-labels.yml: (1) Pinned michalvankodev/copy-issue-labels from mutable tag v1.3.0 to full commit SHA f54e957e58fc976eba5ffa36e1a1030572dbb78d with the tag preserved as a comment. (2) Added a top-level permissions block with 'issues: read' and 'pull-requests: write' — the minimal permissions required for the copy-issue-labels action to read issue labels and apply them to pull requests.

