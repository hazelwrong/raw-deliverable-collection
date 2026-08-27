---
name: raw-deliverable-collection
description: Find and continuously collect publicly available, authentic everyday-work deliverable files for a validated industry-and-occupation matrix. Use when asked to search, collect, or expand a raw inventory of real business deliverables; do not use for task-package design, reference reconstruction, pipeline execution, or evaluation.
---

# Raw Deliverable Collection

Build a reusable inventory of authentic, bounded everyday-work deliverables. The unit is one real work event mapped exactly to one industry and occupation, with one or more original deliverable files. A task package, reference files, prompts, rubrics, conversions, OCR, redaction, and any other downstream processing are outside this skill.

## Start And Resume

1. Use `/Users/hazelwrong/Downloads/raw-deliverable-collection/` as the only inventory root. Create a new `<batch_id>` for this run and resume from its root-level indexes.
2. Read the bundled [task-industry matrix](references/cross_matrix_tasks.md) as the authority for the 33 task types and 9 industries, and the [GDPval occupation taxonomy](references/gdpval-occupation-taxonomy.md) as the authority for the 44 occupations. Record both source versions before collecting formal candidates.
3. Read [the inventory contract](references/inventory-contract.md) before writing records. Compute the current formal count and coverage gaps before choosing sources.
4. Continue collection across batches until exactly 5,000 accepted candidates are present. If a run is interrupted, preserve its batch state so a later invocation resumes from the same inventory.

## Candidate Gate

Accept a candidate only when all of these hold:

- It is an original deliverable from a real, bounded, routine work event, rather than a template, teaching case, policy/manual, marketing item, macro report, or broad strategy document.
- Its task-type and industry pair is allowed by the bundled matrix, and its occupation exactly matches the bundled GDPval occupation taxonomy, with occupational evidence rated A, B, or C. A is direct job-title evidence; B is a documented department, document-type, and duty chain; C is a documented de-identified scenario mapping. Do not admit U (insufficient evidence).
- The source exposes at least one substantive, non-HTML attachment that is itself the target occupation's completed work output. Download and inspect that attachment in its published format. An HTML landing page, notice, result page, or article is provenance evidence only and never satisfies the deliverable requirement by itself.
- The original attachment is publicly downloadable without login, payment, CAPTCHA, anti-bot bypass, or special authorization. Download the original unchanged into the candidate's file directory. URL-only material is a lead and never counts toward 5,000.
- The original publisher or rights-holder page and work context are traceable. Search engines, mirrors, aggregators, social posts, and caches can discover leads but cannot be the formal source.
- Rights/access evidence is recorded file by file or through its landing page. Public access supports internal research and client data annotation only; it does not imply redistribution rights.
- The event has not already been accepted under a different URL, filename, format, or mirror.

Classify every linked attachment by business role before acceptance. Tender/solicitation documents, requirements, policies, templates, blank forms, supplier declarations, applications, and other upstream inputs do not become deliverables merely because they are attached to a result page. If no attachment is a completed target-work output, keep the page as a lead or reject it with `no_substantive_deliverable_attachment`.

Files are preserved exactly as published. Do not redact, sanitize, convert, OCR, execute, unpack for use, or create a derivative of an original file. Inspect only as needed to establish authenticity and metadata. Do not bypass access controls. Preserve publicly accessible original content without copying personal or case details into reports.

## Source And Coverage Strategy

Prefer Chinese sources for each occupation. Before relying on English, exhaust at least three viable Chinese first-party channels and document the attempts; then use English only to fill a real shortage. Favor first-party government, enterprise, industry association, university, hospital, school, public procurement/project, court, and regulator sources with original-publication context.

Treat 80 formal candidates per occupation as the initial floor. Allocate the remaining capacity dynamically: fill occupational gaps first, then missing publisher and document-type diversity, then industry balance. A single publisher may supply at most 20% of an occupation's accepted candidates and a single document type at most 35%; each occupation needs at least three publishers and three document types when supply permits. Total progress takes precedence, but every exception must be recorded.

One event counts once. Use the closest original source as the primary version; attach mirrors and alternate formats as related sources. Separate events only when responsibility, date, or formal decision makes them independently meaningful.

## Collection Loop

1. Select the highest-priority coverage gap and enumerate institutions plus document types, rather than relying on broad occupation keywords.
2. Discover candidates, enumerate every linked attachment, and resolve script-generated download links when this requires only normal public-page behavior. Download likely substantive attachments and inspect enough content to distinguish completed outputs from inputs or supporting evidence.
3. Store source-page HTML under `raw_deliverables/<batch_id>/evidence/landing_pages/<candidate_id>/`. For every accepted deliverable attachment, capture the original filename, MIME type, byte size, SHA-256, source URL, landing URL, acquisition time, and business role; store it under `raw_deliverables/<batch_id>/files/<candidate_id>/`. Keep that candidate directory free of landing-page HTML and non-deliverable attachments.
4. Deduplicate by SHA-256, source URL, title, and real-world event. Link duplicates to the canonical candidate rather than inflating counts.
5. After every 25 newly accepted candidates, report in the active conversation: total accepted, batch accepted, industry/occupation gaps, Chinese/English split, downloaded/lead counts, primary rejection reasons, and the next gap being targeted.
6. Stop accepting exactly at 5,000. Record further qualifying discoveries as `deferred_capacity_reached`; retain rejected and URL-only leads for later human review without counting them.

## Completion

At 5,000 accepted candidates, produce a final inventory-level coverage and deduplication report. State clearly that the inventory contains only raw deliverables and collection metadata, not completed task packages or reference files.
