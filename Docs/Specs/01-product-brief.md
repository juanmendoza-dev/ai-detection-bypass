# Product brief

Status: Draft · Updated: 2026-09-23

## User's starting idea

Build an AI text bypasser: a tool that rewrites AI-generated or AI-assisted text to reduce detection by AI text detectors. Begin with organized specifications and research before implementation.

Confirmed priority targets: GPTZero, Turnitin, and Copyleaks, with D2L Brightspace as the relevant LMS context. See [target detectors and access](06-target-detectors-and-access.md) for verified capabilities and unresolved access requirements. Audience remains unconfirmed.

## First question to answer

Can rewriting consistently reduce detection on selected detectors while preserving facts, meaning, readability, and the writer's intended voice?

This is a hypothesis to test. A result on one detector or a few examples does not establish a reliable product or a universal bypass capability.

## Proposed first version

Confirmed budget: $0. Detection, rewriting, hosting, and compute choices must fit existing resources or verified free allowances. See [zero-budget feasibility](07-zero-budget-feasibility.md).

Start with a small experiment harness, then a simple text rewriting interface if the results justify it. Use an existing language model first; custom model training needs evidence that simpler approaches are insufficient.

Provisional audience: someone editing their own AI-assisted drafts. Audience and intended writing context remain open decisions.

Provisional scope: English prose, pasted text, one document at a time. Input length limits will depend on the selected providers and cost budget.

The proposed interface lets a user:

1. Paste a draft and specify audience, tone, and material that must remain unchanged.
2. Generate a revision.
3. Compare the original and revision and edit the result.
4. Optionally request detector checks when a supported integration is available.
5. Copy the reviewed result.

## Proposed requirements

- Preserve numbers, names, quoted passages, citations, and the substance of claims.
- Do not invent sources or experiences to make text appear more personal.
- Show original and revised text together; preserve the original after errors.
- Identify detector, check date, and score meaning when displaying results.
- Represent unavailable, unsupported, or failed detector checks explicitly.
- Report measured outcomes with their limitations; do not promise universal undetectability or label a detector score as proof of authorship.
- Give users control over whether their text is submitted to a detector service.

## Deferred scope

Custom model training, bulk processing, accounts, billing, document imports, browser extensions, and multilingual support. No stack or provider has been selected.

## Success

Evidence must show useful detector-result changes and acceptable writing quality on unseen documents. Cost, latency, and accessible detector integrations must also support the intended use. Define numerical acceptance targets before the final evaluation; see [the evaluation plan](03-evaluation-plan.md).
