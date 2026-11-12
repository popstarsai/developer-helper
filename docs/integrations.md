# Integration implementation plan

Capabilities were checked against [official sources](sources.md) on 2026-11-11. This document proposes adapters; it does not claim that they have been implemented or tested with live accounts.

## Provider connections

| Provider | MVP ingestion | Later work and limitations |
| --- | --- | --- |
| GitHub | GitHub App installation on selected repositories; REST import; webhooks | Optional PR/check status; separate explicit permissions for agent writes |
| Vercel | Integration authorization; selected account/team projects, deployment metadata, and URLs | Broader domain/billing features only if separately requested |
| Replit | Manual project URL, notes, and user-confirmed link to GitHub | GitHub can track exported/synchronized code; it does not expose all Replit workspace state |
| Lovable | Manual prototype URL and confirmed GitHub link | Git sync provides a code connection; do not assume a general account inventory API |
| X | Store thread URL, user-selected text, and attachments | Full thread retrieval requires a separately validated API/access path; a link alone is not an archived thread |

GitHub App access is separate from signing in to Developer Helper. Start with repository metadata access; request read-only Contents only when the user enables commit/README/license inspection. Installation credentials are minted server-side and scoped to approved repositories. GitHub documents one-hour installation token expiry. [GitHub authentication](https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/authenticating-as-a-github-app-installation)

Use Vercel's integration flow and read scopes for projects/deployments, adding domain read access only if required. Keep account/team identity with every request. Scope selection is part of onboarding; do not fetch environment-variable values for cataloging. [Vercel integration API](https://vercel.com/docs/integrations/create-integration/vercel-api-integrations)

## Sync and categorization

Provider adapters implement capability discovery, authorization, paginated listing, fetching one object, normalization, webhook verification, and disconnect handling. Avoid inventing endpoints for a provider without a documented inventory API; use manual entry instead.

The first import runs in pages and reports progress. Normalize GitHub repository IDs, Vercel project/deployment IDs, canonical URLs, timestamps, default branch, visibility, deployment target, and Git source metadata when available. Missing fields stay unknown. On repository transfers, reconcile an existing stable resource ID to its new account/connection rather than creating a second asset.

Determine relationships in this order:

1. Exact provider IDs and explicit Git-source metadata: record a provider-backed link with evidence.
2. User-supplied relationships: record as confirmed manual links.
3. Matching normalized URLs: propose or confirm only when the identity is unambiguous.
4. Similar names, text, tags, or optional model suggestions: put in a review inbox.

Never combine two projects solely because they share a name. Preserve monorepo root directories and deployment branches; one repository can supply many apps. Avoid fetching full source code during ordinary metadata sync.

For ongoing updates, use authenticated webhooks plus daily reconciliation and a user-triggered sync. Handle pagination, duplicate deliveries, provider throttling, removed permissions, reconnect, rename, and deletion. A last successful sync time must remain visible when a new attempt fails.

## Local companion

A browser application cannot continuously inspect arbitrary local files or another app's internal data. Add an optional macOS companion using Tauri, a local SQLite index, filesystem watchers, and the system Git executable. Pair it with an expiring enrollment flow and a revocable device credential stored in the OS keychain.

Users select folders and choose metadata-only tracking or explicit content upload. Keep absolute filesystem paths local by default. Resolve real paths before access, reject symlink escapes, exclude secrets and generated folders, and debounce file-change bursts. Companion commands use a fixed operation registry and argument arrays rather than executing shell text supplied by a web page.

| Tool | Practical implementation | Boundary |
| --- | --- | --- |
| BBEdit | Track selected files/folders; open them through `bbedit`; add an optional script to save a chosen snippet | Files are the shared data source; unsaved buffers require an explicit editor action |
| Sublime Text | Use `subl` to open files; optional Python plugin sends selected snippets through the paired companion | No automatic capture of all editor buffers |
| Gitfox | Read the same local Git repository with Git CLI; launch Gitfox through its helper where available | No assumed private Gitfox data API; its helper is unavailable in the Mac App Store edition |
| OmniGraffle | Attach exported PDF/PNG; accept sanitized SVG exports where the edition supports them; retain the original `.graffle` file | Preview import is different from reconstructing editable semantic graph edges |
| Obsidian | Write generated Markdown into a selected subfolder of a vault | The web server cannot write directly into an arbitrary local vault |

For Git status, inspect the current branch, HEAD, modified/untracked counts, and recent commit summaries using structured Git output. Handle detached HEAD, empty repositories, worktrees, and absent upstreams. Ahead/behind counts describe locally known refs; display when upstream information was last refreshed. A network fetch is a separate configured action.

OmniGraffle automation can become an optional structured node/edge exporter after a schema and sample files are tested. Do not infer a graph's exact meaning from a raster image. Provide editable captions for sketches and text descriptions alongside diagrams. See the BBEdit, Sublime, Gitfox, and OmniGraffle references in [sources](sources.md).

## NotebookLM export

The first release provides **Prepare for NotebookLM**: generate a Markdown specification and UTF-8 CSV tables, then explain how to add them as sources. Google's current source documentation lists Markdown, CSV, Google Sheets, and other formats. Account limits and support can change, so validate at release time. [Source formats](https://support.google.com/gemininotebook/answer/16215270)

Keep a crucial distinction in the product: generating an export in one click is different from adding it to a remote notebook in one click. The documented notebook/source API is an Enterprise route with licensing and authenticated-user requirements; implement it as a separate optional connector after entitlement checks. Do not depend on undocumented consumer endpoints. [Enterprise notebooks](https://docs.cloud.google.com/gemini/enterprise/notebooklm-enterprise/docs/api-notebooks) · [Enterprise sources](https://docs.cloud.google.com/gemini/enterprise/notebooklm-enterprise/docs/api-notebooks-sources)

Export requirements:

- Use clear section headings, stable asset IDs, source URLs, capture times, and explicit implemented/planned/unknown status.
- Include one project specification per selected project and a combined catalog index for cross-project analysis.
- Put assets and relationships in separate CSVs. Quote fields correctly and escape formula-like spreadsheet cells, including leading `=`, `+`, `-`, and `@` after whitespace/control characters. JSON retains lossless original values.
- Record export schema version, snapshot ID, source counts, file hashes, and any omitted attachments in a manifest.
- Review the selected private notes and attachments before enabling a remote delivery target. Exclude tokens, secrets, and local absolute paths.
- Treat imported notebook sources as snapshots unless a specific connector implements supported refresh behavior. Track exported and delivered states separately.

## Obsidian export and plugin

Start with a downloadable vault-ready folder. Later, the companion writes to a user-selected vault subfolder such as `Developer Helper/`, with a catalog index and stable ID-based project/asset filenames. Include YAML frontmatter (`asset_id`, `provider`, `source_url`, `export_revision`) and relative Markdown links; optionally add Obsidian wikilinks.

Keep generated files separate from user-authored notes. Update only generated files whose prior hash matches the export manifest; otherwise create a conflict copy. Use temporary files and atomic replacement, and do not remove the user's notes when an asset is archived. Repeated exports should not duplicate notes.

A dedicated TypeScript plugin can add **Refresh catalog**, **Attach current note**, and **Open asset** commands through Obsidian's Vault API. Use a narrow, revocable API token; do not embed cloud-provider credentials. Obsidian URIs are useful for opening a destination note, while bulk export should use the companion or plugin. [Vault API](https://docs.obsidian.md/Plugins/Vault) · [Obsidian URI](https://help.obsidian.md/Extending+Obsidian/Obsidian+URI)
