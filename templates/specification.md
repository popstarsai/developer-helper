---
export_schema: "developer-helper/0.1"
project_id: "{{project_id}}"
export_revision: "{{snapshot_id}}"
generated_at: "{{generated_at_iso8601}}"
---

# {{project_name}}

## Purpose

{{user_verified_purpose}}

## Current state

Lifecycle stage: {{stage_or_unknown}}  
Responsible person: {{declared_responsible_person_or_unknown}}  
Last successful provider sync: {{last_successful_sync_or_not_connected}}

| Feature | State: implemented / planned / unknown | Evidence and observation time |
| --- | --- | --- |
| {{feature}} | {{state}} | {{evidence}} |

## Asset inventory

| Asset ID | Name | Type | Provider | URL or local label | Freshness |
| --- | --- | --- | --- | --- | --- |
| {{asset_id}} | {{asset_name}} | {{kind}} | {{provider}} | {{safe_location}} | {{observed_at}} |

## Relationships

| From asset | Relationship | To asset | Confirmed or suggested | Evidence |
| --- | --- | --- | --- | --- |
| {{source}} | {{relation}} | {{target}} | {{status}} | {{evidence}} |

## Technical stack

{{stack_with_sources_and_unknowns}}

## Ownership and access

{{account_ownership_access_responsibility_and_license_observations}}

## Decisions and context

{{selected_notes_and_thread_excerpts_with_source_links}}

## Sketches and diagrams

{{attachment_list_with_text_captions_and_export_omissions}}

## Open questions and next actions

{{open_questions_and_next_actions}}

## Sources and provenance

{{source_urls_capture_times_commit_refs_and_catalog_snapshot}}

## Export notes

This document is a catalog snapshot. Unknowns remain unknown; suggested relationships remain suggestions. Provider access is not a determination of intellectual-property ownership. Secrets and unselected private context are excluded.
