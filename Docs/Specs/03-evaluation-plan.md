# Evaluation plan

Status: Draft · Updated: 2026-09-23

## Experiment question

Does a revision method reduce detection compared with the original and a basic rewrite, while preserving writing quality on unseen documents?

No experiment has run. Sample counts and thresholds below are planning proposals, not results.

The user has confirmed a $0 budget. The 60-document design is a target, not an approved workload: three conditions across two detectors could require 360 checks. First establish permitted access and actual free quotas; if only a small access check is possible, label it accordingly instead of claiming the full pilot completed. See [zero-budget feasibility](07-zero-budget-feasibility.md).

## Dataset

Start with 60 source documents: 20 human-written, 20 generated, and 20 human-edited generated drafts. Keep mixed authorship separate from the binary human/generated comparison. Use material with known provenance and permission to process it.

Include multiple topics, writing styles, lengths, and at least two generation models. Include native and non-native English human controls where provenance supports that description; do not infer author demographics from text.

Split source documents evenly into development and held-out evaluation sets. Keep each original and all its variants in the same split; group related prompts and duplicate sources to avoid leakage. This small pilot can establish feasibility, not substantiate broad marketing claims.

## Comparisons

For each eligible document, compare the unchanged original, one fixed general-purpose clarity rewrite, and the candidate revision method. Use the same inputs and evaluation conditions.

The confirmed targets are GPTZero, Turnitin, and Copyleaks. Start with two accessible targets; GPTZero and Copyleaks are initial API candidates. For transfer testing, reserve a third from method selection if access and budget permit. Turnitin access is not yet established. If only one is available, explicitly limit conclusions to that detector. See [target detectors and access](06-target-detectors-and-access.md).

Treat Brightspace as the delivery context for the configured vendor, not as an additional independent detector. Record API, website, and LMS checks separately until equivalence is established. Separate similarity reports from AI reports. Preserve suppressed/non-numeric results in their original form, and evaluate shared eligible inputs for cross-provider comparisons; report shorter or otherwise ineligible texts separately.

Freeze the candidate method, generation settings, thresholds, and retry budget before the held-out run. Start with one revision per method per document. Any later adaptive experiment needs its own fixed budget and separate report; do not silently keep trying until a favorable result appears.

## Measurements

| Measure | Definition |
| --- | --- |
| Detection rate | Flagged eligible AI-origin documents divided by successfully checked eligible AI-origin documents, separately per detector and authorship category |
| Human false-positive rate | Flagged untouched human controls divided by successfully checked eligible untouched human controls |
| Paired change | Before/after classifications and score changes within each detector, using its documented score meaning |
| Preservation | Reviewer checks for changed claims, numbers, entities, quotes, and citations |
| Readability and voice | Blind, randomized comparison of original and revision; record preference and reasons |
| Cost and latency | Total provider cost, elapsed time, and calls per document, including failures and retries |
| Coverage | Eligible, excluded, failed, and successful checks, with reasons |

Record raw counts alongside rates, confidence intervals for proportions, and paired uncertainty for before/after comparisons. Calculate uncertainty at the source-document level because variants are related. Do not count errors as successful bypasses. Report rewritten human controls separately from untouched human false positives.

Use a human reviewer for every pilot pair, with a second reviewer for a subset and disagreements. Automated similarity scores can help triage but cannot certify factual preservation.

## Required run record

Dataset version; source ID and origin; split; text length; method and prompt version; generation provider/model/settings; detector/version or unknown; timestamp; threshold and score semantics; raw response reference; status/error; latency; cost; quality review. Store benchmark text separately with controlled access.

## Decision gate

Before opening the held-out results, agree on the minimum useful detection-rate improvement, acceptable quality loss, maximum cost, and latency target. Any critical factual corruption disqualifies that output even if the detector score improves.

Proceed to an interface prototype only if the frozen method meets these targets on unseen documents. If the result is uncertain, expand the sample. If it fails, document the result and revise the hypothesis before adding product features. A detector-specific outcome supports only a detector-specific conclusion.
