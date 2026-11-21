# Personal Workspace — Product Vision

Status: Draft for review (2026-11-10). Working title; product name undecided.

## Purpose

A self-hosted, single-user personal workspace replacing the daily functions of Notion, not recreating Notion's universal
database/page builder. The product provides deliberately designed workflows for capture, task management, notes,
knowledge discovery, planning, and eventually leadership and integrations. Data remains portable and recoverable without
the product.

## Product principles

1. **Purpose-built UI**: React pages and dashboards are coded for actual workflows, not configured using a generic page
   builder.
2. **Files first**: user's durable content is held in human-readable Markdown/YAML plus original binary attachments.
   Indexes/caches can be rebuilt.
3. **Capture now, organize later**: typed Inbox items, untyped captures, and one global Scratchpad coexist.
4. **Context across categories**: areas, topics, projects, notebooks, and people provide different views of the same
   objects; most relationships are many-to-many.
5. **Mobile matters**: usable responsive PWA on iPhone/tablet and desktop; online only initially.
6. **Single owner, external automation**: API-first access for AI agents; private information remains protected by
   explicit grants.
7. **Minimum operational complexity**: modular monolith, one server, Docker Compose, private GitHub repo, CI and
   manually triggered deployments.

## Intended workflows

- Capture a thought or URL without classifying it; later promote one capture into one or more notes or tasks.
- Quickly create a task/note directly in Inbox, then refine, link, and organize it.
- Review a Focus list separating today, overdue, flagged, and follow-up actions.
- Work from purpose-built Task Tracker, Weekly Planner, Knowledge Hub, leadership views, and Area pages.
- Keep technical notes with images, code, Mermaid, draw.io previews and attachments, storing ordinary Markdown.
- Link a note to several projects/areas and see it from any relevant context without copying the note.
- Let external agents search and modify allowed data through a controlled API without accessing protected documents by
  default.

## First functional milestone

Inbox + basic Notes + basic Tasks + global Scratchpad, supported by file storage, API, indexing, responsive UI and
automated tests.

## Not goals

- Notion-compatible generic databases, formulas, configurable dashboard builder or real-time multi-user collaboration.
- Kubernetes, microservices, distributed job queues, compulsory Git history of workspace data.
- Full rich calendar application; existing calendars remain authoritative.
- Semantic/vector search or built-in AI chat in the first version.

## Unresolved

Product name; default home screen (`Today` vs `Workspace`); detailed Full Focus System workflows; exact Resource model;
recurring-task history representation; privacy encryption/key handling; specific integrations and rollout schedule.
