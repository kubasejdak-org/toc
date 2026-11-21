# Agent Instructions — Personal Workspace

This file is the **entry point for coding agents**. Read it before proposing or changing code, data formats, UI, tests
or documentation. These rules apply repository-wide. More specific instructions may be added near code later; they must
not silently override accepted product decisions.

## Read first (in order)

1. [`README.md`](README.md) — project map and commands (update as commands become real).
2. [`docs/product/vision.md`](docs/product/vision.md) — goals, boundaries and deliberate non-goals.
3. [`docs/product/requirements.md`](docs/product/requirements.md) — observable product requirements and identifiers.
4. [`docs/product/roadmap.md`](docs/product/roadmap.md) — MVP versus deferred scope.
5. [`docs/architecture/overview.md`](docs/architecture/overview.md) and
   [`docs/architecture/domain-model.md`](docs/architecture/domain-model.md) — selected solution and data contracts.
6. [`docs/architecture/decisions.md`](docs/architecture/decisions.md) — architecture decision records.
7. [`docs/ui/README.md`](docs/ui/README.md) and [`docs/implementation/mvp-plan.md`](docs/implementation/mvp-plan.md) —
   experience guidelines and implementation sequence.
8. [`CHANGELOG.md`](CHANGELOG.md) — user-visible changes.

## Non-negotiable boundaries

- Single-user, self-hosted, **files-first** product. Markdown/YAML/binary assets are authoritative; SQLite is a
  **rebuildable** index, never the sole durable store of user content.
- Explicit, application-defined entity schemas and immutable UUID identities; relationships are stored once and queried
  from either side.
- Purpose-built React UI; **no Notion-like page builder**, general-purpose workflow configuration or microservices
  platform.
- MVP: Inbox, basic Notes and Tasks, global Scratchpad, supporting storage/API/search/mobile foundations. Do not
  implement future modules speculatively.
- One monorepo, one devcontainer for development, Docker Compose for production, GitHub Actions for CI and manual
  deployment.
- Protect content integrity: conditional writes, visible autosave state, in-app conflict resolution, and no silently
  lost drafts.
- Privacy and authentication are design boundaries: never add an unauthenticated production shortcut, reveal private
  metadata, log secrets, or expose application origin to bypass Cloudflare Access.
- Avoid unnecessary dependencies and infrastructure; prefer a simple, testable solution. Agent-initiated destructive or
  security-sensitive actions require explicit user approval.

## Required workflow for every change

1. **Understand** the request and inspect relevant documents and code. Identify affected requirement IDs and accepted
   ADRs. If a material design question is unresolved, make the uncertainty explicit and request a decision rather than
   silently inventing product behavior.
2. **Plan** the smallest coherent vertical slice. State assumptions, affected files, tests and risks. Distinguish a
   provisional implementation choice from an approved architectural decision.
3. **Implement** with validation and error handling. Keep frontend, API, schemas and durable file formats consistent.
   Add or update meaningful automated tests; run focused tests and relevant wider checks.
4. **Synchronize docs in the same change** (see matrix below). Docs are part of Definition of Done, not a separate
   cleanup task.
5. **Report** implementation summary, tests run/results, files/requirements changed, decisions recorded, and known
   limitations. Never claim tests passed if they were not run.

## Documentation update rules

| When changing…                                                                     | Update…                                                                                          |
| ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| User-visible capability, behavior or acceptance criteria                           | `docs/product/requirements.md`, and `docs/product/roadmap.md` if scope/priority changes          |
| Cross-cutting architecture, storage contract, security boundary or major trade-off | New ADR section in `docs/architecture/decisions.md` and affected architecture docs               |
| Entities, fields, relation semantics or deletion behavior                          | `docs/architecture/domain-model.md`, requirements when observable, and an ADR if consequential   |
| Navigation, interaction or design convention                                       | `docs/ui/README.md`, requirements if behavior changes; ADR for lasting architectural UI decision |
| Milestone or delivery plan                                                         | `docs/implementation/mvp-plan.md`, `docs/product/roadmap.md`                                     |
| New setup, dependency, command, entry point or deployment step                     | `README.md` and relevant architecture/implementation docs                                        |
| User-visible added/changed/fixed/removed feature                                   | `CHANGELOG.md` under `Unreleased`                                                                |
| Refactoring with no user-visible behavior change                                   | Usually no changelog entry; update technical docs only if contracts changed                      |

**Requirements format:** follow
[the project's requirements skill](https://github.com/kubasejdak-org/dotfiles-ai/tree/main/claude/skills/requirements)
and its `references/template.md`: grouped sections, checkbox requirements, stable unique IDs (`N.M` within each
section), functional/non-functional/technical sections. Requirements must describe **what users observe**, not class
names, methods, schemas, paths or library choices. Keep agreed future requirements distinct from MVP scope. Never mark
checkbox `done` merely because the requirement was agreed; check only when implemented and verified.

**ADRs:** Append entries using the template in `docs/architecture/decisions.md`. Record context, decision, alternatives,
consequences, status and date. Preserve accepted ADRs as historical records; if changed, append a **new** ADR section
that supersedes an earlier one, then update the index and relevant living architecture docs. Do not create an ADR for
every minor coding choice. ADRs are not a substitute for requirements.

**Changelog:** keep concise, user-facing, under `Unreleased` (`Added`, `Changed`, `Fixed`, `Removed`, `Security`). Don't
log every internal refactor. Do not claim a release exists until it does. Update after actual changes, not merely when
requirements are drafted.

## Verification and safeguards

- Prefer `pytest`, `httpx`, `Vitest`, React Testing Library and `Playwright` as appropriate once tooling is scaffolded;
  commands live in `README.md` when implemented.
- Test file/SQLite reconciliation, schema errors, race/conflict handling, Inbox promotion and autosave failures for
  relevant changes.
- No destructive migration, bulk deletion, cloud deployment, token creation or GitHub write without the user's explicit
  approval.
- Never overwrite files or accepted decisions simply to conform to a new idea without reviewing compatibility and
  migration.
- Do not commit workspace data, credentials, private notes or `.env` secrets to source control.

## At the end of the task

Provide: **what changed**, **what was tested**, **docs updated**, **new or superseded ADRs**, **outstanding decisions**.
If docs are intentionally unchanged, explain why.
