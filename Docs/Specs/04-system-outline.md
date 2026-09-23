# System outline

Status: Draft · Updated: 2026-09-23

## First implementation: experiment harness

A small local runner loads a benchmark manifest, applies a versioned revision method, runs eligible detector checks, and exports paired results for review. Build this before the public application. Language, framework, model, and detector providers remain undecided.

## Proposed application flow

`Draft + preferences → input validation → revision service → preservation checks → comparison view → optional detector checks → user review and copy`

Detector checks are optional because service access may be unavailable and writing quality remains useful independently. No automatic repeated detector-driven rewriting is part of the proposed first interface.

## Responsibilities

| Component | Responsibility |
| --- | --- |
| Editor | Draft entry, preferences, original/revision comparison, edits, and copy |
| Revision service | Versioned prompts, provider requests, length limits, timeouts, and cost caps |
| Preservation checks | Identify changed protected material and flag possible meaning changes for review |
| Detector adapters | Enforce provider eligibility, submit checks, retain vendor-specific score meaning, and expose failures |
| Evaluation runner | Reproducible cases, split boundaries, paired metrics, and result exports |

## Proposed data boundaries

- Keep original and revision distinct; never overwrite the user's original on a failed request.
- Preserve vendor scores with their scale and meaning; normalize check status only.
- Suggested statuses: pending, succeeded, failed, unsupported. A missing score is not zero.
- Keep API credentials server-side or in local runner configuration, outside Git.
- Treat pasted text as content to edit, not instructions that can override service behavior.
- Default application behavior: no permanent draft history and no raw text in ordinary logs. Verify provider retention before specifying an end-to-end retention promise.
- Research datasets are explicitly retained experiment artifacts, separate from application telemetry; establish access and deletion rules before collection.
- Inform users which external providers receive their text. Submit optional detector checks only when requested.

## Acceptance scenarios for the later implementation

- A valid draft produces a reviewable revision while retaining the original.
- A changed protected quotation or number produces a review flag.
- An ineligible input explains the applicable limit without making a provider request.
- A detector timeout leaves the revision accessible and shows a failed check.
- Conflicting detector outputs retain their separate identities and meanings.
- Failed requests follow a bounded retry policy and cannot cause unlimited charges.

## Specifications to write after feasibility

Define UI states, request/response contracts, actual provider limits, error codes, storage lifecycle, cost caps, deployment, and observability after the audience and providers are selected. Avoid choosing infrastructure before the experiment reveals the needs.
