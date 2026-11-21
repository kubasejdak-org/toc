# Roadmap — Draft

## Delivery principles

Each stage results in a locally runnable, testable increment. Future requirements are documented but not prematurely
implemented. No fixed calendar commitments.

### Phase 0 — Product baseline

- Approve requirements, domain model, architecture and unresolved assumptions.
- Establish source repo, devcontainer, automated test strategy and coding conventions.

### Phase 1 — Foundation (technical increment)

- React shell, FastAPI health/API skeleton, SQLite index initialization, file store, UUID, validation, containerized
  local development.
- CI pipeline with representative backend, frontend and browser tests.

### Phase 2 — First useful capture flow

- Raw Inbox capture + categorized quick-create Task/Note.
- Global Scratchpad with autosave and visible persistence state.
- Browse and promote captures safely.

### Phase 3 — Basic Notes and Tasks

- Basic visual editing and Markdown round-trip; Inbox and standard note lists.
- Task lifecycle, priority, deadline/schedule/flag, filters and basic Focus view.
- Optional relations required for this phase, not all possible future entities.

### Phase 4 — MVP hardening and initial deployment

- Global full-text search across implemented types (titles, body text and searchable metadata), with matching excerpts,
  plus relationship browsing.
- Mobile/PWA usability, conflict resolution, failure recovery and E2E paths.
- Docker Compose + Cloudflare Access/Tunnel deployment, backup restore rehearsal.

## Later increments (sequence intentionally open)

- Projects, hierarchical Areas, Topics, Notebooks and broader cross-type relational views.
- Expanded editor: rich attachments, Mermaid, draw.io previews, advanced notes/templates.
- Recurring tasks, delegated work and follow-ups, archive/delete workflows.
- Web Push reminders and external calendar integration.
- Knowledge Hub and advanced contextual discovery.
- Person pages, team/leadership and performance-review workflows, privacy and encryption.
- Full Focus-inspired Weekly / Quarterly Preview, Daily Notes, planning dashboards.
- Azure DevOps, GitHub, reMarkable and homelab integrations; external-agent MCP tools.
- Explicit task delegation to an external Software Factory, with execution status, result review and manual takeover.
- Built-in AI assistant and granular temporary grants to private content.

## Explicitly deferred / not goals

- Generic dynamic page-builder, Notion database clones, realtime multiplayer editing.
- Kubernetes, distributed background queues, mandatory Git versioning of user data.
- Semantic vector search and full offline synchronization.

## Open decisions to revisit by phase

| Decision                                                  | Target moment                   |
| --------------------------------------------------------- | ------------------------------- |
| Exact data type/schema for Resource                       | Before Resources implementation |
| Recurrence persistence/history (reset vs completed files) | Before recurring tasks          |
| Protected document crypto & key management                | Before private-content feature  |
| Home page default and layouts                             | After first working UI          |
| Full Focus planning process and fields                    | Before planning module          |
| Push frequency/default rules                              | Before notifications            |
| Which external calendars and integrations first           | Before integration development  |
