# Developer Helper — product specification

Version: 0.1 proposal  
Reviewed: 2026-11-11  
Repository: https://github.com/popstarsai/developer-helper  
Implementation status: planning only

## Product goal

Help a beginner assemble a reliable record of their development work across tools. A **project** is the product or idea they are pursuing. An **asset** is something involved in that project: a repository, prototype, hosting project, deployment, diagram, conversation, local folder, or specification.

One project can contain many assets; an asset can support several projects. A prototype becoming a deployed app should keep its original context and provenance.

## Main user journey

1. Sign in and create a personal workspace. A sample project explains the interface without requiring a provider connection.
2. Connect GitHub and/or Vercel, select accounts and resources, and preview the import. Manual entry always remains available.
3. Review proposed project groupings and relationship suggestions. Exact provider identifiers can establish links automatically; similarity alone produces a suggestion.
4. Open a project to see its summary, code location, live app, original idea, notes, last sync, and next action.
5. Maintain the same information through a table or a relationship map.
6. Download the project specification or catalog, or send generated notes to a selected local Obsidian folder through the companion.

## Feature requirements

| Feature | Initial behavior | Later extension |
| --- | --- | --- |
| Unified dashboard | Project cards, asset counts, lifecycle stage, last activity, ungrouped inbox, and missing-link indicators | Custom dashboards and team ownership views |
| Automated onboarding | Read-only import of selected GitHub repositories and Vercel projects/deployments; resumable progress | Additional verified provider adapters |
| Dependency map | Typed links, labels, project filtering, keyboard-accessible relationship list | Saved layouts and comparison over time |
| Spreadsheet view | Search, sorting, filters, column visibility, bulk tags, inline edits to user fields, CSV export | CSV import with a dry-run conflict preview; optional XLSX |
| NotebookLM export | One-click generation of Markdown and CSV source files, plus import instructions | Licensed Enterprise API delivery |
| Context | Markdown notes, pasted chat logs, source URLs, and sketch/diagram attachments | Explicitly requested OCR and summaries |
| Local tools | Documented integration contract in MVP | Mac companion for selected folders, snippets, Git metadata, and open-in-editor actions |
| Obsidian | Download a Markdown folder bundle | Companion export into a selected vault; optional dedicated plugin |
| Cloud Mac | Provider and session design in MVP | Paid-session pilot with agent access, build results, and shutdown controls |

## Beginner-facing concepts

- Use labels such as **Code**, **Live app**, **Prototype**, **Idea**, **Notes**, and **Local files**. Technical details appear on demand.
- Explain a relationship in a sentence: “This live app is built from this repository.”
- Show whether a value came from a provider, was entered by a person, or is an unconfirmed suggestion.
- Display **Unknown**, **Not connected**, **Access lost**, **Sync failed**, and **Deleted at source** as different states.
- Show “Needs attention” items such as a deployment with no known repository or a prototype with no recorded code export. These are catalog findings, not judgments about legal ownership.
- Preserve a mobile-friendly list view; graph editing and dense table editing target larger screens.

## Catalog and relationship rules

Asset kinds include `repository`, `hosting_project`, `deployment`, `prototype`, `idea`, `thread`, `conversation`, `diagram`, `document`, `local_repository`, and `local_file`. The provider is a separate field: `github`, `vercel`, `replit`, `lovable`, `x`, `local`, or `manual`.

Relationships include `prototype_of`, `implements`, `built_from`, `deployment_of`, `documents`, `inspired_by`, `depends_on`, and `local_checkout_of`. Store the direction and meaning explicitly. A general graph may contain cycles; a visual arrow is not a claim that all links form a dependency DAG.

Provider metadata is read-only in the first release. User titles, descriptions, stages, tags, owner notes, and project membership are editable and survive synchronization. Archiving a catalog entry does not delete the provider resource.

## Ownership record

Track provider account/team, verified provider access, declared responsible person, optional declared billing owner, source license identifier/link, visibility, canonical source, and export/backup status. Store evidence and observation time with ownership statements. A missing value stays unknown. The application does not infer copyright ownership or license compatibility from an account login, a commit, or an AI-generated claim.

## Export behavior

Generate a specification with purpose, implemented/planned/unknown features, asset inventory, relationships, stack, ownership/access notes, decisions, open questions, and dated source references. Derive it deterministically from stored records. An optional AI rewrite must be opt-in and keep unsupported claims visibly unresolved.

A portable bundle contains `specification.md`, `catalog.csv`, `relationships.csv`, `catalog.json`, an export manifest, and selected attachments. A ZIP packages these files for download; the user imports supported files into NotebookLM after extraction. No remote upload is implied by generating a bundle.

## Scope and release criteria

The first usable release includes authentication, manual cataloging, GitHub/Vercel synchronization, table and map views, notes/attachments, and exports. Local filesystem access, paid cloud sessions, agent execution, and direct Enterprise notebook publishing follow separately.

Proposed MVP acceptance targets, to be measured during development:

- A new user can import and organize a small account into a first project in under five minutes, excluding provider authorization delays.
- Repeating an import or replaying a webhook does not duplicate assets or erase user notes.
- Provider outages produce a visible stale state without falsely marking resources deleted.
- Every export is attributable to a catalog revision and preserves source URLs and unknowns.
- Tenant isolation, attachment access, webhook authentication, and CSV formula escaping pass targeted tests.
- A workspace with 10,000 assets remains usable with server-side paging; a project graph initially loads at most 200 visible nodes and expands on request.

See [architecture](docs/architecture.md), [integrations](docs/integrations.md), and [roadmap](docs/roadmap.md) for implementation details.
