# Developer Helper

A home for the ownership stack of agentic development: the ideas, prototypes, repositories, deployments, files, and decisions that make up a project.

Designed for beginner developers who want to answer: **What have I made, where is it, how does it connect, and what can I do next?**

## Project status

**Architecture and implementation plan; application development has not started.** The integrations, interfaces, and cloud environments below are planned capabilities, not running services. No provider accounts or paid infrastructure have been provisioned.

## Planned experience

- Add GitHub repositories, Vercel apps, Replit and Lovable projects, sketches, X threads, and chat notes to one catalog.
- Import selected GitHub and Vercel resources and keep provider metadata current.
- Switch between a dashboard, editable table, and map of project relationships.
- Export portable Markdown, CSV, and JSON; prepare sources for NotebookLM and notes for Obsidian.
- Use an optional Mac companion for local files, Git status, BBEdit, Sublime Text, Gitfox, and OmniGraffle exports.
- Later, start a budgeted cloud Mac session, give a coding agent access to its project, and collect builds and changes back into the catalog.

The catalog distinguishes account ownership, access permissions, billing responsibility, and recorded licensing information. Access to a repository alone does not establish ownership of its contents.

## Recommended foundation

Next.js and TypeScript; Tailwind CSS and shadcn/ui; Supabase Postgres, Auth, and Storage; TanStack Table; React Flow; Inngest for background jobs. Add a Tauri companion and a provider-neutral cloud Mac adapter after the web MVP.

## Build documents

| Document | Purpose |
| --- | --- |
| [specification.md](specification.md) | Product behavior, release scope, and success criteria |
| [Architecture](docs/architecture.md) | Stack, boundaries, data flows, and proposed source layout |
| [Data model](docs/data-model.md) | Tables, relationships, constraints, and ownership records |
| [Integrations](docs/integrations.md) | Sync, desktop applications, NotebookLM, and Obsidian |
| [Cloud Mac design](docs/cloud-mac.md) | Provider evaluation, Xcode access, lifecycle, and cost controls |
| [Roadmap](docs/roadmap.md) | Ordered milestones and acceptance gates |
| [Specification export template](templates/specification.md) | Suggested structure for a generated project document |
| [Sources](docs/sources.md) | Official references checked on 2026-11-11 |

Start implementation with the foundation and manual catalog milestones in the roadmap. Contributions can begin with the catalog UI, sample fixtures, database policies, connector normalization, or export formatting. Keep pull requests focused on one milestone and distinguish working features from mocks.

## License

[Apache License 2.0](LICENSE). The existing repository license is retained.
