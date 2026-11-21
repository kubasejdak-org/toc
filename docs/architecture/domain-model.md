# Domain Model — Draft

## Design principles

- Types have **application-defined schemas**, not arbitrary user-defined properties. Fields may be optional and omitted
  in YAML.
- Each entity is a file with UUID filename and matching frontmatter `id`; the Markdown body is available where
  meaningful.
- Relations are stored **once** in a designated owner document and can be navigated/edited from either side through an
  index.
- Most relationships are N:M; hierarchical parent relations are exceptions. Paths are not identities.
- Archive is orthogonal to lifecycle status. Private is orthogonal to Area membership.

## Entity inventory

| Type          | Core purpose                             | Initial release? | Notes                                                     |
| ------------- | ---------------------------------------- | ---------------- | --------------------------------------------------------- |
| Note          | Freeform knowledge and journals/meetings | Yes (basic)      | Variants are templates and optional fields; shared schema |
| Task          | Action, planning, delegation, recurrence | Yes (basic)      | Nested tasks and checklists are distinct                  |
| Project       | Goal-oriented grouping and progress      | Later            | Many-to-many Area and Task relations                      |
| Area          | Hierarchical scope/responsibility        | Later            | Custom-coded per-area views are possible                  |
| Topic         | Controlled label vocabulary              | Later            | One shared YAML dictionary; no empty per-topic documents  |
| Notebook      | Logical collection of notes              | Later            | N:M note membership                                       |
| Person        | Optional durable person profile          | Later            | Family or work; not a login account                       |
| Team          | Optional domain grouping for people      | Later            | Not a user permission group                               |
| Resource      | Saved external item                      | Later            | Representation still under review                         |
| Inbox capture | Raw uncategorized material               | Yes              | Promoted into one or more independent typed objects       |
| Scratchpad    | Single global unstructured page          | Yes              | One durable Markdown document                             |
| Attachment    | Binary asset referenced by content       | Basic as needed  | UUID file and original filename manifest                  |

## Task fields (conceptual)

- `status`: `inbox`, `to_refine`, `backlog`, `in_progress`, `done`.
- `priority`: `low`, `normal` (default), `high`, `critical`.
- `due_date`: deadline; `scheduled_date`: intended work day; `day_preference`: `any`, `weekday`, `weekend`.
- `flagged`: short-horizon attention, independent of priority.
- `follow_up_date`: when owner should check progress, distinct from due/scheduled.
- `assignees`: list of either stable Person references or literal names, with grouping possible by displayed name.
- `parent_task`: at most one; child tasks are regular Task objects.
- `recurrence`: rule, initially prefers a single task whose status and next date are reset on completion. Missed
  instances do not accumulate. History is not required for MVP.
- `archived`, `private`: independent concerns.
- Markdown body may include a checkbox list but those are _not_ child Task records.

## Relationships (initial candidate ownership)

| Relationship               | Canonical storage owner | View from reverse side            |
| -------------------------- | ----------------------- | --------------------------------- |
| Note → Projects            | Note                    | Project lists linked Notes        |
| Note → Notebooks           | Note                    | Notebook lists Notes              |
| Task → Projects            | Task                    | Project lists Tasks               |
| Task → parent Task         | Child Task              | Parent lists children             |
| Project → Areas            | Project                 | Area lists projects               |
| Area → parent Area         | Child Area              | Parent lists subareas             |
| Note/Task/Project → Topics | Referencing entity      | Topic shows tagged objects        |
| Task → assignees           | Task                    | Person page / name-based grouping |

This ownership table is a **proposal for implementation review**, not a claim that all relationships have already been
resolved. Reverse-side editing updates the canonical owner only. Names shown in UI are resolved via stable IDs.

## Files and IDs

```text
workspace/
  notes/<uuid>.md
  tasks/<uuid>.md
  projects/<uuid>.md
  areas/<uuid>.md
  people/<uuid>.md
  notebooks/<uuid>.md
  resources/<uuid>.md
  inbox/<uuid>.md
  topics.yaml
  scratchpad.md
  attachments/<uuid>.<extension>
  attachments/manifest.yaml
```

Paths are illustrative. The ID in an object's filename never changes when its title changes. Attached original names are
preserved in the manifest.

## Inbox promotion

1. Raw capture stays intact during conversion.
2. User chooses one or more target object types and edits target fields.
3. New object(s) get new UUIDs and are saved/validated.
4. Source is removed only after successful completion (or kept if desired by UI).

## Deletion and archive

- `done` ≠ `archived`; filters can show all completed or active only.
- Archive is a separate discovery view; done tasks may additionally appear as cleanup candidates.
- No Trash initially; external backups are recovery mechanism.
- Project deletion defaults to unlink only. Optional delete of exclusive project tasks, not shared tasks; note deletion
  is never implicit.
- Parent task deletion asks whether child tasks should be deleted or detached.
- Other cascading behaviors are deferred; protect against dangling references.

## Privacy

An object-level privacy rule takes precedence over any implicit defaults from Area. Private frontmatter might reveal
confidential metadata; a privacy design is required before enabling encrypted documents or exposing them to agents.
