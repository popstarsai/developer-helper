# Development roadmap

Planning estimate: **6–8 engineer-weeks for a web MVP**, then **2–3 for a Mac companion** and **2–4 for a cloud Mac pilot**. This assumes one experienced full-stack engineer, managed services, and available provider accounts. Provider approvals, broad desktop distribution, signing/release features, and production hardening can extend the schedule. These are estimates, not completed milestones.

## 0. Foundation — week 1

- Scaffold Next.js/TypeScript, pnpm workspaces, shared validation, and a responsive shell.
- Create Supabase development environments, SQL migrations, membership policies, and private buckets.
- Configure local environment documentation and GitHub Actions for type checks and focused tests.
- Add a clearly labeled fictional demo dataset representing an idea, prototype, repository, hosting project, deployment, and local checkout.

**Exit:** two test users cannot read or mutate each other's records or attachments. The demo is usable without provider credentials.

## 1. Manual catalog — week 2

- Build project/asset CRUD, tags, archive/restore, notes, attachment uploads, and the ungrouped inbox.
- Implement table search/filter/sort/pagination, inline user-field edits, record-version conflicts, and mobile cards.
- Add ownership/access fields with unknown and evidence states.

**Exit:** a beginner can manually capture a prototype, link its repository and live app, attach a sketch, and later find each item.

## 2. GitHub and Vercel — weeks 3–4

- Register provider applications and implement authorized account/resource selection.
- Build paginated imports, stable-ID normalization, provider metadata views, and resumable progress.
- Implement signature verification, event receipts, outbox delivery, background reconciliation, rate-limit handling, and reconnect.
- Build the relationship review inbox; automatically link only provider-backed identities.

**Exit:** import twice without duplicates; preserve notes through rename/reconnect; detect webhook replay; survive partial pagination and expired credentials without falsely reporting deletion. Verify a monorepo with multiple deployments.

## 3. Maps and exports — week 5

- Render typed relationships with React Flow, a selected-asset drawer, and an equivalent accessible list.
- Collapse deployment history, filter by project/type, and allow manual relationship creation and rejection of suggestions.
- Build deterministic Markdown/CSV/JSON exports from consistent snapshots, including checksums and source provenance.
- Add NotebookLM import guidance and a vault-ready Obsidian bundle.

**Exit:** exported files preserve IDs, source links, unknown values, multiline notes, and Unicode. Spreadsheet formula-like text is escaped. A generated sample imports successfully through the documented NotebookLM flow on a test account.

## 4. Beginner beta — week 6, with weeks 7–8 as iteration buffer

- Test onboarding with several beginner developers and revise labels, empty states, progress, and recovery messages.
- Check keyboard navigation and mobile layouts; profile a 10,000-asset fixture and bounded project graphs.
- Add error monitoring, redacted logs, connection-health indicators, quotas, export/delete flows, and backup recovery documentation.
- Verify Markdown/SVG previews, private download expiration, authorization checks, and workspace removal.

**Exit:** complete the end-to-end journey from sign-in to import, project grouping, relationship review, and export. Finish a database-plus-file restore exercise. Mark the web MVP released only after these gates pass.

## 5. Mac companion — 2–3 additional weeks

- Implement paired device enrollment, keychain credentials, folder picker, local SQLite index, and debounced file tracking.
- Read local Git status and commits; handle empty repositories, worktrees, missing remotes, and offline operation.
- Add BBEdit/Sublime open actions and optional explicit snippet capture; use Gitfox's helper where installed.
- Accept OmniGraffle PDF/PNG/SVG exports and retain source files.
- Write Obsidian exports into a selected managed subfolder, using hash checks and conflict copies.
- Sign/notarize a limited pilot build; allow additional time for general distribution and support.

**Exit:** selected-folder access is enforced across symlinks and restarts; revoked devices stop syncing; repeated vault export preserves user edits. The web catalog still works without a companion.

## 6. Cloud Mac pilot — 2–4 additional weeks

- Complete the Namespace provider spike and record the result in an architecture decision.
- Implement capability checks, lifecycle persistence, budgets, idempotent create, task execution, and cleanup reconciliation.
- Run an agent inside the guest; validate Xcode MCP and ordinary build paths on a pinned image.
- Return patches, logs, and artifacts as project assets with commit/toolchain provenance.
- Exercise the failure matrix in [cloud-mac.md](cloud-mac.md).

**Exit:** a user starts an authorized, budgeted session, receives a successful build or actionable failure, and can verify compute has stopped. No abandoned session remains unaccounted for.

## 7. Optional extensions after validation

Dedicated Obsidian plugin; NotebookLM Enterprise publishing; additional provider inventory APIs; CSV import; optional AI classification and summaries; explicit release/signing workflows; team ownership handoffs; and a catalog MCP server exposing scoped read/export operations.

Prioritize these from observed usage. A generic agent orchestrator, automated public publishing, and provider billing resale are separate product expansions.

## First implementation slice

Build **sign in → add a project → add repository/live-app links → attach a note → inspect the table → export specification.md**. This makes the ownership model testable before background synchronization or paid execution is introduced.
