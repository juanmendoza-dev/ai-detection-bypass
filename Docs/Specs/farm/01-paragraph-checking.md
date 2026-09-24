# Paragraph checking

Status: Draft · Updated: 2026-09-23

Scope clarification: this document describes the assistant-proposed quota-aware alternative, not the account-creation farm the user subsequently clarified. See [the requested lifecycle](README.md#requested-access-mechanism-and-feasibility). Its implementation milestones are proposals, not an approved handoff to an engineer.

## First slice

Accept one plain-text document, preserve its original content, divide it into paragraphs, and let the user select paragraphs and detectors for checks. Show each result beside the exact text submitted. No rewriting, LLM calls, adaptive optimization, or web application is required for this slice.

Initial delivery is proposed as a local runner with structured input and JSON/CSV exports. Language and storage format remain implementation decisions.

## Processing flow

`Document → paragraph extraction → detector eligibility → user-selected checks → queue → adapter → stored result → comparison report`

1. Preserve the original document and assign a document ID and content hash.
2. Split at blank lines, including whitespace-only blank lines. Treat consecutive nonblank lines as one paragraph. Support LF and CRLF line endings without modifying the source.
3. Record paragraph order, exact source text, and start/end offsets. Define offsets as zero-based Unicode code-point indices with an exclusive end. Separators remain recoverable from the original document.
4. Skip empty spans. Do not silently split long paragraphs, join short ones, pad text, or remove citations to satisfy provider limits.
5. Evaluate each selected paragraph against the chosen adapter's verified eligibility rules before submitting anything.
6. Queue only eligible checks for which access and free allowance are established. Submit only to the selected providers.
7. Store raw vendor output and display its documented meaning with provider, surface, scan mode, and timestamp.

The same paragraph in a revised document is a new text version. Preserve earlier versions and link comparisons explicitly rather than overwriting results.

## Eligibility and granularity

Provider configuration records supported input types/languages, minimum and maximum lengths, length units, access surface, scan mode, and the source/date of the rules. Unknown eligibility blocks automatic submission pending verification. Character, byte, token, and word limits must not be treated as interchangeable.

A paragraph can be too short for a detector even when the complete document is eligible. Report that as `ineligible`, with a reason. The existing [target research](../06-target-detectors-and-access.md) documents Turnitin length and access constraints; verify applicable requirements before implementation or live use.

An optional later whole-document check is a separate job with separate eligibility. Never average paragraph scores into a document score, interpret missing results as zero, or claim that passing every paragraph establishes a whole-document outcome. Preserve non-numeric and suppressed vendor results as returned.

Brightspace is an access context for its configured detector. Record the actual vendor and distinguish AI reports from similarity reports.

## Adapter contract

Each adapter exposes:

- Capabilities and eligibility rules, including whether it supports an authorized automated submission route or manual import only.
- Access readiness and known quota state; an available website alone is insufficient evidence of supported automation.
- Submission and, where required, asynchronous polling with bounded attempts.
- Parsing into a common status envelope while retaining vendor-specific result semantics.

Manual imports must identify the exact submitted text, provider, report type, access surface, scan mode if known, and check date. Reject attribution to a paragraph when text identity cannot be established. Store unknown model/version fields explicitly; do not invent them.

Mocks are for software verification only. Mark them as synthetic and exclude them from all performance summaries.

## Job lifecycle and limits

Proposed states: `queued`, `running`, `succeeded`, `ineligible`, `blocked_access`, `blocked_quota`, `failed`, and `cancelled`.

- Begin with one worker and one active request per provider. Concurrency increases require verified provider support.
- Reserve a known quota unit before dispatch so queued jobs cannot overspend the allowance. If quota is unknown, block automatic dispatch until it is established.
- External spend must remain $0. Disable paid fallback and do not attach payment-backed trials.
- On quota exhaustion, pause that provider's pending work. Resume only after a documented renewal or verified allowance update; do not infer renewal from a fresh session.
- Retry transient failures at most twice, honoring provider retry timing and counting attempts toward the run budget. Do not retry eligibility, authentication, or quota failures automatically.
- If a timed-out submission may have consumed quota, retain that uncertainty. Reconcile through supported status lookup before resubmission; otherwise require review.
- A failed check on one paragraph must not discard completed checks. A restart must preserve job state and avoid duplicate submissions.
- Cancellation stops pending work; an already submitted request may still complete or consume allowance.

## Cache behavior

Cache identity includes exact submitted-text hash, detector, access surface, scan mode, exposed model version (or `unknown`), adapter version, and request settings. Keep account/entitlement context separate where it could affect results.

Reuse is limited to the same experiment run by default. Cross-run reuse must be explicit and show the original check time, because hidden vendor updates can change behavior even with identical settings. Cached results are not fresh measurements or additional independent samples.

## Minimum records

| Record | Required fields |
| --- | --- |
| Document | ID, version, original-text reference, hash, provenance, creation time |
| Paragraph | ID, document/version, order, source offsets, exact-text reference/hash, measured lengths |
| Run | ID, selected providers/paragraphs, configuration version, attempt budget, start/end time |
| Job | ID, run/paragraph IDs, provider/surface/mode, request settings, state/reason, attempts, timestamps, quota reservation |
| Result | Job ID, real/synthetic origin, raw-response reference, native label/score/scale, semantics, model/version or unknown, check time, latency, cost or unknown, cache origin |

Keep credentials outside Git. Keep raw text and vendor responses out of routine logs. Experiment artifacts are deliberately retained locally; document their location and deletion procedure. Do not commit private drafts or reports. Sending text externally requires the user's selection of that provider; provider retention must be established before live checks.

## Report behavior

Show each paragraph in source order with one result entry per selected detector. Every entry must show either an actual result or an explicit state and reason. Identify cached, imported, and synthetic results visibly.

Summaries count successful, failed, ineligible, and blocked checks separately. Keep vendor scores separate. Paragraphs from the same document are related observations; any later effectiveness analysis must account for source-document grouping under the existing evaluation plan.

## Implementation milestones

1. **Paragraph extraction and records:** local input, stable versioned records, exact text recovery, and export; no external services.
2. **Queue and mock adapter:** eligibility, budgets, state persistence, cancellation, and failure handling. Demonstrates orchestration only.
3. **Manual result import:** attach real reports to exact inputs and generate a comparison report. Does not claim automated access.
4. **First supported live adapter:** choose a provider only after verifying account entitlement, permitted access route, limits, score semantics, and data handling. Run a small access smoke test within its known allowance.
5. **Additional providers and document comparison:** add independently verified adapters and optional whole-document checks. Keep unavailable targets explicitly untested.

Each milestone should be independently reviewable. Do not build all integrations or a rewriting engine before the first slice works.

## Acceptance examples

- A document with blank lines and wrapped lines produces the expected ordered paragraphs; offsets recover exact source text, including Unicode and CRLF cases.
- A short paragraph remains visible as ineligible for a provider; no request is made and its text is not padded.
- Exhausted allowance blocks pending jobs without dropping previous results or creating replacement accounts.
- A repeated identical job within a run reuses its result and identifies the cache origin.
- Restarting after an uncertain submission does not blindly submit it again.
- A vendor timeout yields a bounded failure state; another provider's completed result remains available.
- An imported similarity report cannot become an AI detection result; synthetic results cannot enter real-result metrics.
- A report with paragraph checks alone makes no claim about whole-document classification.

## Decisions before live implementation

Establish the first provider and actual account allowance, supported automation route, writing context, permission to transmit samples, and provider retention. The coordinator needs no LLM; any later rewrite method and its compute requirements are a separate feature.
