# AGENTS.md

This file provides context and instructions for AI coding agents working on the **duolingo-readme-stats** project.

## Project Overview

**duolingo-readme-stats** is currently a documentation-first repository that defines the renderer architecture for README-ready Duolingo SVG stats cards.

Current documentation scope emphasizes:

- SVG output as the primary renderer contract.
- League-based visual variants (Bronze through Diamond).
- Explicit sync metadata with a 1-hour cadence.

## Tech Stack

| Area                              | Details                                           |
| --------------------------------- | ------------------------------------------------- |
| Repository state                  | Documentation-first (Markdown + Mermaid diagrams) |
| Target runtime (architecture)     | Node.js 22 LTS                                    |
| Target language (architecture)    | TypeScript 5                                      |
| Planned framework (architecture)  | Fastify                                           |
| Planned validation (architecture) | Zod                                               |
| Planned deployment (architecture) | Vercel serverless + hourly Vercel Cron            |

## Repository Structure

```text
duolingo-readme-stats/
├── README.md          # Top-level project summary and scope
├── ARCHITECTURE.md    # Source of truth for renderer module design and constraints
└── AGENTS.md          # Agent-specific operating guidance (this file)
```

## Architecture Conventions

- Treat `ARCHITECTURE.md` as the technical source of truth.
- Preserve the facade + focused-submodules design:
  - `renderer-facade`
  - `style-resolver` + `league-style-map`
  - `layout-engine`
  - `ornament-engine`
  - `sync-meta-composer`
  - `svg-builder` + `error-renderer`
- Keep league token definitions centralized; avoid scattering style conditionals.
- Keep sync-cadence policy explicit and consistent (`nextSyncAt = syncedAt + 1 hour`).
- Preserve league taxonomy ordering exactly:
  `Bronze -> Silver -> Gold -> Sapphire -> Ruby -> Emerald -> Amethyst -> Pearl -> Obsidian -> Diamond`.
- Maintain fallback behavior expectations for unknown/null league values.

## Common Commands

This repository does not currently define build, lint, or test pipelines. Use lightweight documentation workflow commands:

```sh
# View issue context
gh issue view <issue-number> --repo utilForever/duolingo-readme-stats --comments

# Inspect local changes
git --no-pager status --short
git --no-pager diff
```

## Commit Style

- Conventional Commits: `feat:`, `fix:`, `refactor:`, `perf:`, `test:`, `docs:`, `chore:`
- Split commits by behavior or another meaningful unit of change.
- Release commits: `feat: vX.Y.Z — short summary`
- Hotfix: `fix: description` (no version in message)

## Contribution Guidelines

- Keep changes tightly scoped to the requested issue.
- Do not claim implemented runtime behavior that is not present in the repository.
- Keep terminology aligned between `README.md`, `ARCHITECTURE.md`, and `AGENTS.md`.
- When editing league-related guidance, verify ordering and naming consistency.
- When editing sync metadata guidance, keep the 1-hour cadence language unchanged unless the architecture spec is intentionally updated.
- Keep commits focused and write clear commit messages.
- Open a pull request targeting the `main` branch.
