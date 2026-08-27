# Inventory Contract

## Directory Layout

```text
/Users/hazelwrong/Downloads/raw-deliverable-collection/
  cross_matrix_tasks.md
  inventory.jsonl
  accepted_candidates.json
  rejected_candidates.json
  deferred_candidates.json
  lead_candidates.json
  channel_registry.json
  coverage_report.json
  raw_deliverables/<batch_id>/
    batch_manifest.json
    evidence/landing_pages/<candidate_id>/
      <original-source-page.html>
    files/<candidate_id>/
      <original-deliverable-attachment>
```

`inventory.jsonl` is append-only. The JSON files are materialized views that may be rebuilt from it; never discard the source records. Original filenames and bytes must remain unchanged. HTML source pages belong in `evidence/landing_pages`; only verified deliverable attachments belong in `files`.

## Candidate Record

Use a record with these fields. Add fields only when evidence requires them; do not duplicate source-file content in metadata.

```json
{
  "candidate_id": "cand-000001",
  "batch_id": "20260826T093000Z-a31f",
  "status": "accepted",
  "industry": "exact matrix label",
  "occupation": "exact matrix label",
  "language": "zh",
  "scenario_summary": "short, non-sensitive description of the bounded work event",
  "deliverable_title": "published title",
  "document_type": "inspection record",
  "event_date": "2026-08-26 or null",
  "publisher": "original publisher",
  "publisher_type": "government",
  "source_url": "direct original-file URL",
  "landing_url": "original publication/context page",
  "occupation_evidence_level": "A",
  "occupation_evidence": "job title, duty chain, or de-identified mapping rationale",
  "authenticity_evidence": "why this is a real delivered work artifact",
  "acquisition_status": "downloaded",
  "rights_status": "public_internal_research_only",
  "rights_evidence_url": "copyright or source page URL",
  "files": [
    {
      "relative_path": "raw_deliverables/<batch_id>/files/cand-000001/original.pdf",
      "original_filename": "original.pdf",
      "mime_type": "application/pdf",
      "size_bytes": 12345,
      "sha256": "...",
      "artifact_role": "deliverable",
      "downloaded_at": "2026-08-26T09:30:00Z"
    }
  ],
  "duplicate_of": null,
  "related_sources": [],
  "matrix_path": "/absolute/path/cross_matrix_tasks.md",
  "matrix_sha256": "...",
  "collected_at": "2026-08-26T09:30:00Z"
}
```

Accepted records require `acquisition_status=downloaded` and at least one verified, non-HTML original attachment with `artifact_role=deliverable`. A landing page or downloaded HTML page is evidence, not an accepted file. `lead`, `rejected`, and `deferred_capacity_reached` records must carry a reason and may omit file details. Use `login_required_metadata_only`, `restricted_or_unclear`, `unavailable`, or `no_substantive_deliverable_attachment` for leads/rejections, but never count them as accepted.

## Rights And Evidence

Use one of these values in `rights_status`:

- `open_license`: an explicit reusable license is evidenced.
- `public_internal_research_only`: publicly downloadable, retained only for internal research/client data annotation; no redistribution claim.
- `restricted_or_unclear`: accessible context exists but rights or download suitability is unclear.
- `login_required_metadata_only`: extra authorization is required.
- `unavailable`: the source no longer provides the original.

Record the page or document that supports the status. Do not infer an open license from public access alone.

## Evidence Levels

- `A`: title block, signature, author credit, or workflow explicitly identifies the target job.
- `B`: organization/department, document type, recipient, and business action form a defensible duty chain to the target job.
- `C`: an otherwise authentic de-identified file supports a documented scenario mapping, though an individual job title is absent.
- `U`: the evidence is too weak. Keep it as a lead or reject it; never accept it.

Monitor A/B/C counts by occupation. C may represent no more than 40% of an occupation's accepted candidates, except with a recorded, temporary supply exception during collection; resolve exceptions before final completion.

## Deduplication And Reporting

Treat matching SHA-256 values as the same file. Also review shared source URLs, titles, organizations, dates, and event descriptions for event-level duplicates. A canonical record carries related URLs and formats.

`coverage_report.json` must show accepted count, 5,000 target, per-industry and per-occupation counts and gaps, language split, publisher/document-type concentration, A/B/C distribution, rights-status distribution, downloaded count, leads, rejections, deferred records, and duplicate links.

Use `batch_manifest.json` to record batch start/end, matrix path/hash, selected coverage gaps, source channels attempted, accepted/rejected/lead/deferred counts, errors, and the next resume priority.
