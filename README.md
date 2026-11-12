# Personal Workspace — Project Specification

**Status:** Draft documentation package, 2026-11-10. This folder contains specifications and working agreements, **not a
functioning application**.

A single-user self-hosted workspace replacing selected Notion workflows, with files-first user-owned Markdown/YAML
content, portable attachments and a purpose-built responsive UI. **First functional increment:** Inbox, basic Notes and
Tasks, global Scratchpad.

## Start here

1. **For the product owner:** review [`docs/product/requirements.md`](docs/product/requirements.md), then
   [`docs/product/roadmap.md`](docs/product/roadmap.md). Mark ambiguous or missing behavior; checkboxes indicate
   _implemented and verified_, not _approved_.
2. **For an agent:** read [`AGENTS.md`](AGENTS.md) before modifying any file. It is the navigation and maintenance
   contract.
3. **For architecture review:** read [`docs/architecture/overview.md`](docs/architecture/overview.md),
   [`docs/architecture/domain-model.md`](docs/architecture/domain-model.md) and the
   [`ADR index`](docs/architecture/decisions.md).
4. **For implementation:** read [`docs/implementation/mvp-plan.md`](docs/implementation/mvp-plan.md), then start with
   milestone M0 after owner approval.

## Documentation map

| File                                                                     | Responsibility                                                                                                                                                         |
| ------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`AGENTS.md`](AGENTS.md)                                                 | AI-agent reading order, workflow, documentation and testing obligations                                                                                                |
| [`CHANGELOG.md`](CHANGELOG.md)                                           | User-visible implemented changes                                                                                                                                       |
| [`docs/product/vision.md`](docs/product/vision.md)                       | Purpose, success and non-goals                                                                                                                                         |
| [`docs/product/requirements.md`](docs/product/requirements.md)           | Functional/non-functional/technical requirements, grouped per [requirements skill](https://github.com/kubasejdak-org/dotfiles-ai/tree/main/claude/skills/requirements) |
| [`docs/product/roadmap.md`](docs/product/roadmap.md)                     | MVP/deferred scope and release phases                                                                                                                                  |
| [`docs/architecture/overview.md`](docs/architecture/overview.md)         | Current design and technical boundaries                                                                                                                                |
| [`docs/architecture/domain-model.md`](docs/architecture/domain-model.md) | Entities, relations, deletion, storage naming                                                                                                                          |
| [`docs/architecture/decisions.md`](docs/architecture/decisions.md)       | ADR log: consequential decisions, rationale and trade-offs                                                                                                             |
| [`docs/ui/README.md`](docs/ui/README.md)                                 | UX, editor and responsive interaction guidelines                                                                                                                       |
| [`docs/implementation/mvp-plan.md`](docs/implementation/mvp-plan.md)     | Incremental milestones and acceptance checks                                                                                                                           |
| [`docs/engineering/documentation.md`](docs/engineering/documentation.md) | How documents evolve without duplication                                                                                                                               |

## Planned technology (not yet scaffolded)

GitHub monorepo; one devcontainer for Python/uv and Node/npm; FastAPI REST; React/TypeScript/Vite/shadcn/ui;
Markdown/YAML file store and SQLite indexing; Docker Compose deployment on Linux; Cloudflare Access/Tunnel; GitHub
Actions (pytest, Vitest and Playwright), GHCR, manual release.

**No run/test/deploy commands exist yet**. They must be documented here when M0 scaffolding implements them. Do not use
the development auth bypass in a production deployment.

## Review workflow and next step

1. Review/annotate product requirements for completeness and acceptance clarity; prioritize
   Inbox/Notes/Tasks/Scratchpad.
2. Review architecture model and ADR choices; resolve MVP-blocking questions.
3. Approve M0 milestone; coding agent scaffolds repository and adds verified development commands and CI.
4. Continue one vertical slice at a time, updating requirements/ADRs/README/changelog as outlined in `AGENTS.md`.

Unresolved design issues are documented in the existing requirements, roadmap, UI guide, implementation plan and
architecture overview. Do **not** treat a draft as implicit approval to implement all future functionality.

## Additional planned capabilities

- Global full-text search with matching excerpts is part of the MVP.
- Future task integration may explicitly delegate work to an external Software Factory; this is not part of the initial
  MVP.
