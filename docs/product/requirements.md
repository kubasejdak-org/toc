# Personal Workspace – Requirements

Status: Draft for stakeholder review, 2026-11-10. Grouped format per the `requirements` skill in
`kubasejdak-org/dotfiles-ai`. Unchecked boxes represent requirements to implement, not rejected decisions. See
`roadmap.md` for scope.

## Overview

A personal, self-hosted workspace for capturing, organizing and retrieving notes, tasks and related information on
desktop and mobile. It replaces selected Notion workflows with purpose-built interfaces while keeping user-owned content
portable. The initial release concentrates on Inbox, Notes, Tasks and Scratchpad; the remaining capabilities are
confirmed direction unless marked open.

## Functional Requirements

### 1. Capture and Inbox

- [ ] **1.1**: The user can quickly capture free-form text, URLs and supported attachments without choosing a final
      content category.
- [ ] **1.2**: The user can create an already-categorized note or task directly in Inbox, with minimal mandatory fields.
- [ ] **1.3**: Inbox displays pending captures and categorized items awaiting review, grouped or filtered by category.
- [ ] **1.4**: The user can promote one uncategorized capture into one or more categorized items; each resulting item
      has an independent identity.
    - The original capture is retained until all requested items are successfully saved; it can then be removed.
- [ ] **1.5**: The user can revisit an Inbox item, supply missing details and remove it from Inbox.
- [ ] **1.6**: The user has one globally accessible Scratchpad for unstructured content without mandatory classification
      or review status.

### 2. Notes and editing

- [ ] **2.1**: The user can create, view, modify, archive and delete notes with optional structured metadata.
- [ ] **2.2**: The user edits notes in a visual, Notion-style editor rather than being required to edit Markdown syntax.
- [ ] **2.3**: The editor provides slash commands, automatic formatting shortcuts, headings, lists, checklists, quotes,
      links, images and highlighted code blocks.
- [ ] **2.4**: The editor displays link previews with recognizable site icons where available and supports links to
      internal objects.
- [ ] **2.5**: The editor supports displayed Mermaid diagrams with editable diagram definitions.
- [ ] **2.6**: The editor displays draw.io diagrams stored as editable attachments; editing in an external tool is
      sufficient initially.
- [ ] **2.7**: The user can start a note from a template/variant, such as meeting, journal or general note, with
      optional variant-relevant fields.
- [ ] **2.8**: Changes to text content, including Scratchpad, are saved automatically with visible saving, saved and
      error states.
- [ ] **2.9**: The user can attach, access and download files while preserving their original download names.

### 3. Tasks and personal planning

- [ ] **3.1**: The user can create and manage tasks in Inbox, To Refine, Backlog, In Progress and Done.
- [ ] **3.2**: Tasks have optional priority levels Low, Normal, High and Critical, independent from planning dates and
      flagging.
- [ ] **3.3**: The user can independently specify a deadline, a planned execution day, an optional preferred day
      category (any/weekday/weekend), and a flag for near-term attention.
- [ ] **3.4**: Tasks can contain ordinary checklists and can also have full child tasks, including nested children.
- [ ] **3.5**: A task can be related to multiple projects, areas, notes and other supported objects.
- [ ] **3.6**: Focus and task views distinguish tasks due today, scheduled today, overdue and flagged, with distinct
      visual cues; completed tasks are not shown as overdue.
- [ ] **3.7**: The user can assign tasks to named people without being required to create a Person entry for every
      assignee.
- [ ] **3.8**: The user can group project tasks by assignee name even when a named assignee has no Person profile.
- [ ] **3.9**: The user can set independent follow-up dates for delegated tasks and clearly distinguish a follow-up
      action from performing the task.
- [ ] **3.10**: The user can manage recurring tasks without accumulating a new overdue item for each missed occurrence;
      completion advances to the next valid future date.
- [ ] **3.11**: The user can view completed tasks in context, exclude them from active views, and selectively archive or
      delete them.

### 4. Organization and relationships

- [ ] **4.1**: The system supports distinct, predefined categories of content, including notes, tasks, projects, areas,
      topics, notebooks, people and resources.
- [ ] **4.2**: A content item can be connected to multiple applicable items of another category; the same relationship
      is visible and editable from either side.
- [ ] **4.3**: The user can organize Areas hierarchically and browse either just the selected area or that area
      including all descendant areas.
- [ ] **4.4**: A project can belong to multiple areas, and a note can be associated with multiple projects or notebooks.
- [ ] **4.5**: The user can select topics from a consistent shared vocabulary rather than creating inconsistent copies
      of the same label.
- [ ] **4.6**: People may represent family members, colleagues or other relevant contacts; a Person profile is optional
      for a person merely named in a task.
- [ ] **4.7**: Users can access specialized, purpose-built pages that combine relevant information from multiple
      categories, including specific area pages.
- [ ] **4.8**: The user can mark supported content as archived, find it in an Archive view, and restore or permanently
      delete it.
- [ ] **4.9**: Deleting a project does not silently delete related notes or shared tasks; the user can optionally delete
      tasks exclusive to that project after an explicit warning.
- [ ] **4.10**: Deleting a task with children offers a choice between deleting child tasks and keeping them
      independently.

### 5. Search and knowledge discovery

- [ ] **5.1**: The user can search across supported content categories by title, full body text and searchable metadata
      by entering a query in a global search field, without first navigating to individual pages or lists.
- [ ] **5.2**: Each matching result identifies its content category and title, and shows a relevant excerpt from
      matching body text when available, highlighting matched terms. Selecting a result opens the corresponding item.
- [ ] **5.3**: Search results can be filtered by category and contextual relationships, including an area and its
      descendants.
- [ ] **5.4**: Search results and navigation respect private-content access restrictions.
- [ ] **5.5**: The Knowledge Hub provides a combined discovery surface rather than requiring the user to search notes,
      projects and resources separately.

### 6. Privacy, access and data control

- [ ] **6.1**: Only the owner can sign in and use the application; people named in the data are not application users.
- [ ] **6.2**: The owner can mark individual supported items private; new content created in a privacy-designated area
      adopts an appropriate default, without weakening existing content protections if area links change.
- [ ] **6.3**: Private content requires additional controlled access before disclosure; protected data is excluded from
      unauthorized search and API responses.
- [ ] **6.4**: The owner can grant an external agent explicit, revocable, optionally time-limited permissions to
      selected private data, with read and write permissions separately controlled.
- [ ] **6.5**: The user can recover and migrate their content using backed-up files, without depending on the
      application to decode a proprietary content database.
- [ ] **6.6**: The user can remove content permanently without needing an application-level Trash; backups remain an
      independent recovery mechanism.

### 7. Notifications and external systems

- [ ] **7.1**: The user can receive push notifications for tasks through the installed web application where supported
      and authorized by the device.
- [ ] **7.2**: The user can configure general reminder rules as well as individual task reminders, independently of task
      scheduling and deadlines.
- [ ] **7.3**: The user can view events from connected external calendars alongside planned tasks, without managing a
      duplicate internal event calendar.
- [ ] **7.4**: Supported integrations can both read external information and perform permitted remote actions;
      availability of actions depends on each integration.
- [ ] **7.5**: External agents can search and update allowed workspace content through an authenticated machine
      interface.

### 8. Usability and safeguards

- [ ] **8.1**: The application is usable on desktop, tablet and phone, with layouts suited to each form factor.
- [ ] **8.2**: When content has changed since editing began, the system prevents silent overwrite and offers an in-app
      way to compare and resolve the conflict.
- [ ] **8.3**: A failed save clearly reports failure and retains unsaved edits for retry while the current editing
      session remains available.
- [ ] **8.4**: Content can be retrieved and edited through normal application workflows without requiring direct
      manipulation of storage files.

### 9. Purpose-built planning and leadership views (post-MVP)

- [ ] **9.1**: The user can review daily plans and upcoming weeks from purpose-built pages combining tasks, notes and
      external calendar events.
- [ ] **9.2**: The user can perform structured weekly and quarterly reviews inspired by the Full Focus planning
      methodology, with the exact review content to be agreed before implementation.
- [ ] **9.3**: The user can browse selected team members through a dedicated leadership view with related one-to-one
      notes, follow-ups, tasks and periodic evaluations.
- [ ] **9.4**: The user can relate notes and important dates to family members without requiring work-specific
      evaluation fields on person profiles.

### 10. External integration and extensibility (post-MVP)

- [ ] **10.1**: The user can see relevant external work items, such as review requests, alongside workspace content,
      without requiring every external record to become a local note.
- [ ] **10.2**: The user can relate local content to external items using persistent references, even if the external
      data cache is rebuilt.
- [ ] **10.3**: The user can access selected workspace operations using external agent tools; a future embedded
      assistant may use the same capabilities.
- [ ] **10.4**: The user can explicitly delegate an eligible task to an external Software Factory and view its execution
      status, results and errors in the task context.
    - Delegation is opt-in for each task; a task remains usable even if no Software Factory is configured.
    - The user can inspect the resulting work and retain control over accepting completion or taking over the task.
    - The integration must not automatically mark a task Done merely because an external execution finished.

## Non-Functional Requirements

### 1. Data integrity and recoverability

- [ ] **1.1**: Failed or interrupted writes must not leave partially written content as the authoritative document.
- [ ] **1.2**: An index or cache may be discarded and rebuilt from the durable user data without loss of user-owned
      content.
- [ ] **1.3**: A conflict must not silently overwrite a newer persisted version of content.
- [ ] **1.4**: Periodic consistency verification must detect externally changed or invalid content and report unresolved
      errors.

### 2. Security and privacy

- [ ] **2.1**: Unauthorized requests must be denied even if traffic bypasses the expected browser navigation route.
- [ ] **2.2**: Private content must not be inadvertently disclosed through titles, search indexes, logs, previews or
      agent operations.
- [ ] **2.3**: Secrets and credentials must not be included in source control or user-content exports.
- [ ] **2.4**: Operations performed with external-service privileges must be restricted to explicitly authorized
      capabilities.

### 3. Reliability and usability

- [ ] **3.1**: The application must clearly identify lack of network connectivity and must not falsely indicate
      successful save or offline synchronization.
- [ ] **3.2**: The core capture and editing workflows must work through a mobile browser installed as a PWA.
- [ ] **3.3**: The owner must be able to recover a working deployment from a consistent backup of durable content and
      configuration.
- [ ] **3.4**: Core features must remain usable when optional external integrations are unavailable.

## Technical Constraints and Requirements

### 1. Data and platform

- [ ] **1.1**: Durable owned content shall be stored in portable Markdown with structured frontmatter and ordinary
      binary attachments; SQLite shall serve only as a rebuildable index/cache.
- [ ] **1.2**: Objects shall have stable immutable UUIDs for identity, relationship references, file naming and API
      addressing.
- [ ] **1.3**: Data files shall be organized by object category, independent of area/project membership.
- [ ] **1.4**: Attachments shall be stored centrally under stable IDs with a durable mapping to original filenames.
- [ ] **1.5**: The application shall use a modular-monolith backend with a REST API and React-based web/PWA frontend.

### 2. Hosting and development

- [ ] **2.1**: Deployment shall use Docker Compose on a single Linux server; Kubernetes is excluded.
- [ ] **2.2**: External access shall use one domain protected by Cloudflare Access and Tunnel, with server-side token
      verification.
- [ ] **2.3**: The application shall be online-only in the initial implementation.
- [ ] **2.4**: Source shall live in a private GitHub monorepo, with CI tests and image builds and manual deployment of
      selected releases.
- [ ] **2.5**: Development tools and application processes shall run inside a devcontainer without requiring
      project-specific Python/Node installations on the host.
- [ ] **2.6**: Automated testing shall include backend unit/integration tests, frontend component tests and focused
      browser E2E tests.

## Clarifications / not yet finalized

- Exact recurring-task implementation: one resettable task (preferred for MVP), with no separate SQL history; distinct
  completed files remain an alternative.
- Full resource content model, archive defaults per type, and list of initially implemented entity types.
- Encryption/key lifecycle, private-content indexing, and delegated-access implementation details.
- Default home page and final purpose-built page compositions.
- Exact reminder defaults, thresholds, access-token policies and initial calendar provider.
- Detailed Full Focus System, Team Management and other future integrations.
