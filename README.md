# Atlas — Enterprise Agent Portal

> **Demo repository** for the talk *“A Supply Chain for Agent Context.”*
> This repo plays the role of **Atlas Corp’s internal portal** of org‑approved AI‑agent context.

It is the **single trusted source** for the skills, prompts, and rules that every Atlas team’s
coding agent should use — versioned, hash‑verified, and governed by an org policy. Teams don’t
copy‑paste standards from a wiki; they **source** them from here with the
[Agent Package Manager (APM)](https://microsoft.github.io/apm/).

## What’s inside

| Path | What it is |
| --- | --- |
| [`skills/secure-coding/`](skills/secure-coding/) | Atlas secure‑coding standards (input validation, secrets, dependencies). |
| [`skills/pr-review/`](skills/pr-review/) | The Atlas pull‑request review checklist. |
| [`skills/api-standards/`](skills/api-standards/) | Atlas REST/API design conventions. |
| [`apm-policy.yml`](apm-policy.yml) | The org **baseline policy** — trusted sources + pinned versions, enforced in CI. |

Each skill is a plain directory with a `SKILL.md`. That’s the whole package format — no build step.

## Consume it (any harness)

Add the packages you need to your project’s `apm.yml`, pinned to a released version:

```yaml
name: orders-service
version: 2.4.0
targets: [copilot, claude, cursor]
dependencies:
  apm:
    - webmaxru/apm-enterprise-portal-demo/skills/secure-coding#v1.0.0
    - webmaxru/apm-enterprise-portal-demo/skills/pr-review#v1.0.0
    - webmaxru/apm-enterprise-portal-demo/skills/api-standards#v1.0.0
includes: auto
```

Then restore identical, hash‑verified context on every machine and harness:

```bash
apm install
```

## Govern it

CI verifies that every dependency comes from a **trusted source** and is **pinned** to a version:

```bash
apm audit --ci --policy webmaxru/apm-enterprise-portal-demo
```

Exit `0` when clean; exit `1` (PR blocked) on an unpinned or off‑policy dependency.

---

*Fictional company, real tooling. Built for a live demo; safe to fork and explore.*
