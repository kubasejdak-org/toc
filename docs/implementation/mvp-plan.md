# MVP Implementation Plan — Draft for Agent Review

This is a proposed execution sequence, not an instruction to immediately implement all stages. Requires review of
`product/requirements.md`, `architecture/domain-model.md`, `architecture/overview.md` first.

## Working agreement

- For each milestone: confirm design boundaries, implement a vertical slice, run focused automated tests and document
  decisions.
- Do not introduce new domain types, database ownership or background infrastructure merely to anticipate future
  modules.
- Treat storage and migrations as high-risk: add file corruption, conflict, restart and recovery tests early.
- Definition of done for a stage: feature usable end to end, tests pass, no silently failed writes, documentation
  synchronized.

## M0 — Repository and environment

Deliverables: private monorepo scaffolding; devcontainer with Python/uv, Node/npm and Playwright dependencies; FastAPI
and React/Vite/shadcn projects; formatting/lint/test scripts; GitHub Actions skeleton; Compose deployment baseline.

Acceptance:

- Fresh clone opens in devcontainer without requiring host-installed project dependencies.
- Frontend and backend run with hot reload; Python debugger attaches and stops at a breakpoint.
- A minimal browser E2E smoke test passes locally and in CI.

## M1 — Durable file store and API foundations

Deliverables: typed model registry and validation; UUID-named Markdown with frontmatter; stable revision checks; atomic
writes; SQLite indexing/rebuild; HTTP errors/validation; basic authorization boundary.

Acceptance:

- Create/read/update/delete a sample Note through API and inspect its Markdown file.
- Change title without renaming UUID file; rebuild index with equivalent retrieved content.
- Concurrent stale revision is rejected without data loss.
- Index or interrupted-save fault is detected and recoverable without losing authoritative user content.

## M2 — Raw Inbox, quick-create and Scratchpad

Deliverables: capture editor, Inbox list, categorized quick-create for notes/tasks, promotion to one or more objects;
global Scratchpad autosave.

Acceptance:

- Capture an untyped thought and later create two new objects from it.
- Source capture cannot disappear if any requested creation failed.
- Create a note or task directly in Inbox on phone-size viewport.
- Scratchpad displays Saving/Saved/Failed accurately; no false success after a simulated backend outage.

## M3 — Basic Notes and Tasks

Deliverables: editor proof-of-concept with round-trip Markdown, note templates baseline, task lifecycle,
priority/due/scheduled/flag, task list filters and initial Focus.

Acceptance:

- User edits a heading, list, checklist and link visually, saves, reopens and sees equivalent content.
- Different task dates display correct today/overdue state; `done` tasks are not highlighted as overdue.
- User filters tasks by status/priority and can return to completed tasks.

## M4 — Navigation, search, conflict UX and deployment

Deliverables: cross-type FTS for supported categories; responsive navigation; explicit conflict resolution; Cloudflare
Access/Tunnel deployment guide, Compose release workflow; smoke tests and backup/restore checklist.

Acceptance:

- Search finds a phrase in an eligible note and excludes inaccessible data.
- Two tabs editing same note trigger in-app conflict handling; neither draft silently disappears.
- PWA loads over HTTPS on supported mobile devices.
- Manual deployment pins a known image version; backup restore can regenerate index.

## Test matrix

- `pytest`: models, recurrence logic when implemented, relations, validation, recovery.
- `pytest + httpx`: HTTP lifecycle, revision conflicts, indexing and Inbox promotion.
- `Vitest + React Testing Library`: capture form, state indicators, task filters.
- `Playwright`: capture → promotion, Scratchpad save/failure, note edit/refresh, conflict, mobile viewport.

## Explicit non-MVP items

Comprehensive project/area/notebook/person modules; recurring tasks; advanced WYSIWYG blocks, Mermaid/draw.io; encrypted
private notes; Web Push; calendar/DevOps integrations; deep agent authorization/MCP; Full Focus workflows.

## Risks and review gates

1. **Editor selection**: prototype and validate fidelity before expanding rich-text feature scope.
2. **Storage semantics**: document whether YAML metadata and Markdown body are preserved across external edits and round
   trips.
3. **Atomicity**: filesystem and SQLite cannot share a simple transaction; test reconciliation and retries.
4. **Conflict safety**: prevent lost drafts in autosave and offline/error states, despite online-only scope.
5. **Security**: do not expose development auth bypass in deployed environment; protect backend origin from direct
   public access.
