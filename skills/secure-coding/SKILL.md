---
name: secure-coding
description: Atlas secure-coding standards for AI coding agents. Use when writing, reviewing, or refactoring code that handles user input, secrets, authentication, database access, or third-party dependencies in an Atlas service. Enforces input validation, no hardcoded secrets, parameterized queries, least-privilege, and pinned dependencies. Don't use for non-Atlas projects or for general security research unrelated to a code change.
license: MIT
metadata:
  author: Atlas Platform Engineering
  version: "1.0"
---

# Atlas Secure-Coding Standards

Apply these rules to every code change. They are the Atlas baseline; a service may tighten them, never loosen them.

## Inputs and data
- Validate and normalize all external input at the boundary. Reject by default; allow-list what is expected.
- Use parameterized queries or an ORM. Never build SQL, shell, or HTML by string concatenation.
- Encode output for its sink (HTML, URL, shell, SQL) to prevent injection.

## Secrets and configuration
- No secrets in source, logs, or error messages. Read them from the platform secret store at runtime.
- Fail closed: if a secret or required config is missing, refuse to start rather than falling back to a default.

## Authentication and authorization
- Check authorization on every request at the server, not just in the UI.
- Prefer short-lived tokens and least-privilege scopes. Never log tokens or full credentials.

## Dependencies (supply chain)
- Add dependencies only from Atlas-approved sources. Pin every dependency to a version or hash.
- Do not introduce a new transitive tool or MCP server without review.

## When you cannot comply
State the rule you are breaking, why, and the compensating control — in the PR description. Do not silently skip a rule.
