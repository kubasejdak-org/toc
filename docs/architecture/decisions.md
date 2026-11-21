# Architecture Decision Records (ADR)

This is the **single architecture decision log** for the project. Each record has a stable ID, date, status, context,
decision, alternatives, consequences and follow-ups. This log captures **why** choices were made; the living
architecture documents describe the current implementation.

## Index

| ID                    | Decision                                                | Status   |
| --------------------- | ------------------------------------------------------- | -------- |
| [ADR-0001](#adr-0001) | Files First and rebuildable search index                | Accepted |
| [ADR-0002](#adr-0002) | Immutable identity and canonical relationship ownership | Accepted |
| [ADR-0003](#adr-0003) | Purpose-built UI instead of generic page builder        | Accepted |
| [ADR-0004](#adr-0004) | Single user with Cloudflare access boundary             | Accepted |
| [ADR-0005](#adr-0005) | Monorepo, devcontainer, Compose and manual deployment   | Accepted |
| [ADR-0006](#adr-0006) | Raw Inbox capture becomes new typed objects             | Accepted |

## Workflow

- Append a new `ADR-NNNN` section for a consequential architecture decision, assigning the next sequential ID.
- Start unapproved decisions with **Status: Proposed**. Only mark **Accepted** after owner approval.
- Never silently rewrite an accepted historical decision. Add a new record with **Supersedes: ADR-NNNN**, mark the old
  record **Superseded by ADR-NNNN**, and update current architecture documents.
- Do not create an ADR for routine implementation choices or duplicate requirements here.

## Template for new entries

```markdown
### ADR-NNNN: Title

- **Status:** Proposed
- **Date:** YYYY-MM-DD
- **Related requirements:** Relevant section/IDs
- **Supersedes:** ADR-NNNN (optional)

#### Context

#### Decision

#### Alternatives considered

#### Consequences

#### Follow-ups
```

---

### ADR-0001: Files First and rebuildable search index

- **Status:** Accepted
- **Date:** 2026-11-10
- **Related requirements:** See `docs/product/requirements.md` (cross-cutting constraints)

#### Context

User data should be portable, recoverable from backups and usable by future tools without a proprietary primary
database.

#### Decision

Persist owned records as Markdown with YAML frontmatter and attachments as ordinary files. Maintain SQLite as a
rebuildable index/cache for relationships, search and views. Use the application API for normal writes; reconcile
changes made outside it periodically and offer manual reindexing. No Git-backed user-data history in MVP.

#### Alternatives considered

A primary SQL database was rejected as source of truth. Continuous file watching was rejected in favor of API-driven
writes plus periodic verification.

#### Consequences

Backup and migrations center on files. File writes and SQLite updates cannot form a single physical transaction:
explicit recovery/reconciliation and failure tests are required.

#### Follow-ups

Finalize data schema migration rules and resilient backup snapshot process.

---

### ADR-0002: Immutable identity and canonical relationship ownership

- **Status:** Accepted
- **Date:** 2026-11-10
- **Related requirements:** See `docs/product/requirements.md` (cross-cutting constraints)

#### Context

Objects may belong to many Areas, Projects and Notebooks, and links must be navigable from both directions without
duplicating authority.

#### Decision

Each typed record has an immutable UUID as its filename and frontmatter ID. A relationship is stored once in the
designated owner record; the index exposes reverse lookups and editing from either side. Most associations are
many-to-many; parent hierarchies have one parent per child.

#### Alternatives considered

Paths or titles as identity, and storing the same relationship in both records, were rejected.

#### Consequences

Renaming titles does not break links; writes from reverse views must update the canonical owner. Referential integrity
checks and deletion behavior must be implemented and tested.

#### Follow-ups

Finalize canonical ownership for each additional relation when its entity type is implemented.

---

### ADR-0003: Purpose-built UI instead of generic page builder

- **Status:** Accepted
- **Date:** 2026-11-10
- **Related requirements:** See `docs/product/requirements.md` (cross-cutting constraints)

#### Context

The owner is a developer using AI coding agents and wants a polished workflow-specific product, not a system for
configuring arbitrary pages at runtime.

#### Decision

Use explicitly coded React pages and reusable components. Support different desktop and mobile layouts. Main navigation
is oriented around workflows (Inbox, Task Tracker, planning, knowledge, leadership), with Area pages as separate
contextual views.

#### Alternatives considered

A configurable block dashboard or Notion-like page builder was rejected. Navigation exclusively by record type was also
rejected.

#### Consequences

New workflow pages require code changes, in exchange for simpler product logic and greater control of UX.

#### Follow-ups

Final homepage layout remains open until tested in an actual UI.

---

### ADR-0004: Single user with Cloudflare access boundary

- **Status:** Accepted
- **Date:** 2026-11-10
- **Related requirements:** See `docs/product/requirements.md` (cross-cutting constraints)

#### Context

The app holds personal and potentially sensitive content but is intended for one owner, accessible on multiple devices
and externally without router port forwarding.

#### Decision

Use a canonical hostname through Cloudflare Access and Tunnel. No separate application login screen in the initial
product; backend must validate the Access identity token and protect API and origin against bypass. Domain Person and
Team records are not accounts.

#### Alternatives considered

Own username/password login and multi-user roles were rejected for MVP. A separate LAN auth route was rejected.

#### Consequences

Deployment depends on Cloudflare availability, and access protection requires correct policy, origin and token
verification. External agents need separate constrained credentials. Private-document unlocking/encryption remains a
separate future security design.

#### Follow-ups

Before any public deployment validate token verification, direct-origin access, MFA policy, machine access and security
tests.

---

### ADR-0005: Monorepo, devcontainer, Compose and manual deployment

- **Status:** Accepted
- **Date:** 2026-11-10
- **Related requirements:** See `docs/product/requirements.md` (cross-cutting constraints)

#### Context

One developer with coding agents needs straightforward debugging, CI and a low-maintenance homelab deployment.

#### Decision

One private GitHub monorepo; one devcontainer containing Python/uv and Node/npm. Run FastAPI and Vite as development
processes inside it. Use GitHub Actions for tests and images (GHCR), Docker Compose on one Linux server for production,
and manually trigger deployment of selected versions.

#### Alternatives considered

Multiple repository layout, multiple default devcontainers, Kubernetes and automatic production deployment were
rejected.

#### Consequences

Debugging is direct, dependencies stay off the host, and delivery remains operator controlled. Keep deployment
repeatable and data storage outside containers.

#### Follow-ups

Implement runnable commands and exact image/version rollback procedure during scaffolding.

---

### ADR-0006: Raw Inbox capture becomes new typed objects

- **Status:** Accepted
- **Date:** 2026-11-10
- **Related requirements:** See `docs/product/requirements.md` (cross-cutting constraints)

#### Context

Rapid Inbox capture allows unclassified text that may later become a note, task or multiple records.

#### Decision

Conversion creates one or more newly identified typed objects; do not mutate a raw capture into a different entity type
in place. Keep the source until target writes have succeeded. Separately, quick-create of a typed item can put it
directly into Inbox.

#### Alternatives considered

Mutating the type of an existing record while retaining its UUID was rejected.

#### Consequences

Conversion is explicit, schema-safe and supports one-to-many outcomes. Partial failure must not lose source content; a
repeat operation must avoid accidental duplicates or clearly surface the state.

#### Follow-ups

Finalize exact UX for retry after partial target creation in the Inbox implementation phase.

---
