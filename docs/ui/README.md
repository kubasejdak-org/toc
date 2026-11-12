# UI / UX Design — Living Guide (Draft)

## Intent

Purpose-built, visually polished workspace for **desktop, tablet and phone**. This is not a user-configurable page
builder. UI changes happen in React code, composed from reusable primitives.

## Navigation and views

- Navigation centers on **workflows**, not a separate sidebar entry for every schema type.
- Planned contextual pages: Inbox, Task Tracker, Focus, Weekly Planner, Full Focus workflow, Knowledge Hub, Team
  Management, global Scratchpad, and Area-specific pages.
- Areas form a hierarchy; a selected Area can optionally include descendants. Specific Areas may have uniquely coded
  views.
- **Home page intentionally undecided**: compare a `Today` dashboard with a `Workspace` portal after a working
  prototype.
- Compact mobile layout can differ from desktop, not merely shrink desktop columns. Online-only PWA.

## Editing

- Notes use a visual block-oriented editor, Notion-like slash commands (`/`) and Markdown typing shortcuts (`### ` for a
  heading; checkbox syntax for a task list).
- Users are not expected to edit Markdown source. Markdown is the durable interchange format: test parse -> edit -> save
  -> reload fidelity.
- Basic formatting, hyperlinks, images/attachments and code blocks; site favicon for external links as UI decoration.
- Future: Mermaid render/edit; `.drawio` preview linked to the editable external source file. No arbitrary embedded
  dynamic database views in notes initially.
- Autosave shows Saving / Saved / Failed. On conflict, preserve local draft and offer in-app version comparison/merge,
  not manual file repair.

## Tasks and attention

- `Low / Normal / High / Critical` priority is **not** a daily focus indicator.
- Distinguish a hard deadline, intended execution day, day preference and `flagged` near-term attention.
- Today items have a **green** visual cue; overdue items **red**; other items neutral. Completed tasks are not
  highlighted overdue.
- Follow-up items appear in Focus with a label indicating **ask/check progress**, not **perform task**.
- Views can choose to include completed tasks, while archived items stay out of normal views by default.

## Prototype and acceptance strategy

Build and test a focused vertical slice of Inbox → capture → Note/Task, Scratchpad, basic task list, note editing and
error/conflict handling at desktop and mobile viewports. Revisit actual layout and home page only after seeing the
running UI.

## Open design questions

- Homepage default and information density.
- Final mobile navigation pattern.
- Detailed Inbox conversion and conflict resolution interactions.
- Actual editor engine and supported Markdown dialect after round-trip spike.
- Full Focus and Leadership page composition: design when their modules are scheduled.
