---
name: pr-review
description: The Atlas pull-request review checklist for AI coding agents. Use when opening a pull request or reviewing one in an Atlas service — to self-review a diff, write the PR description, or leave review comments. Covers correctness, tests, security, API compatibility, and rollout/observability. Don't use for non-Atlas repositories or for unrelated code-explanation tasks.
license: MIT
metadata:
  author: Atlas Platform Engineering
  version: "1.0"
---

# Atlas Pull-Request Review Checklist

Review the diff like a staff engineer. Comment on what matters; skip style nits a linter already catches.

## Correctness
- Does the change do what the PR says, and only that? Flag unrelated drive-by changes.
- Are edge cases and error paths handled? Look for unchecked nulls, empty collections, and timeouts.

## Tests
- New behavior has tests; fixed bugs have a regression test that fails without the fix.
- Tests assert behavior, not implementation details.

## Security
- Apply the Atlas `secure-coding` standard. Flag untrusted input, secrets, and new dependencies.

## API and data compatibility
- Public API and schema changes are backward compatible, or gated behind a version/flag.
- Database migrations are reversible and safe to run before the code deploys.

## Rollout and observability
- The change is safe to roll back. Risky changes sit behind a feature flag.
- New failure modes emit a log or metric an on-call engineer can act on.

## PR description
Summarize **what** changed and **why**, the risk, and how it was tested. Link the issue.
