# Documentation lifecycle

Use [`AGENTS.md`](../../AGENTS.md) as the normative checklist for agents. This page explains the different document
roles.

| Artifact              | Purpose                                             | Update when                                                      |
| --------------------- | --------------------------------------------------- | ---------------------------------------------------------------- |
| Product vision        | Product rationale, audiences, boundaries            | Goals or non-goals shift                                         |
| Requirements          | Observable behavior, testable acceptance            | Feature behavior/scope changes                                   |
| Roadmap               | Phase and MVP scope                                 | Priorities or release boundaries change                          |
| Domain model          | Entities, relationships, fields                     | Durable domain contract changes                                  |
| Architecture overview | Current system design                               | Architectural implementation evolves                             |
| ADRs                  | _Why_ a consequential decision was made             | New accepted architectural trade-off or a decision is superseded |
| UI guide              | Interaction, workflow and responsive conventions    | UX conventions are agreed or changed                             |
| MVP plan              | Implementation sequence and verification            | Delivery plan changes                                            |
| README                | How to onboard, run, test, deploy and navigate docs | Repo commands or structure change                                |
| CHANGELOG             | Changes experienced by users                        | Features are actually added, modified, fixed or removed          |

**Requirements are the contract; ADRs are the rationale; architecture docs are the current design; changelog is the
implemented history.** Avoid duplicate normative descriptions. Link from one document to another instead of copying
sections.

## Requirements workflow

Follow [requirements skill](https://github.com/kubasejdak-org/dotfiles-ai/tree/main/claude/skills/requirements) and
bundled template. Keep one grouped requirements document unless a genuinely separate large feature needs its own
specification. Do not grow docs by repeating observations; split ambiguous behavior into independently testable
requirements and explicitly label deferred scope.

## ADR process

1. Discuss decision and alternatives with the owner.
2. Append an ADR section with status `Proposed` while awaiting approval. Do not promote a proposal to `Accepted` without
   agreement.
3. On acceptance, update the index in `decisions.md` and current architecture documents together.
4. If reversing a choice, append a new ADR section with a supersedes reference, mark old superseded, and assess
   compatibility/data migration.

## Review gate before implementation

Owner reviews requirements and open questions first, then the architecture/ADR baseline, then milestone acceptance
criteria. Implementation should proceed incrementally with docs and tests included in each change.
