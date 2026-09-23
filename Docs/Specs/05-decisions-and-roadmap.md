# Decisions and roadmap

Status: Draft · Updated: 2026-09-23

## Confirmed instructions

| Decision | Basis |
| --- | --- |
| Specifications live in `Docs/Specs` | User request |
| Begin with planning and research | User request |
| Current project budget is $0 | User explicitly confirmed; applies to detectors and other project services |
| Explore an AI text bypasser | User's stated product idea |
| Prioritize GPTZero, Turnitin, and Copyleaks; include D2L Brightspace as the LMS context | User's target list; platform distinction documented in [target research](06-target-detectors-and-access.md) |

## Proposed defaults

English prose; personal draft editing as the provisional audience; an existing language model; an evaluation harness before a web interface; no custom training initially. These defaults keep the first experiment small and can change as requirements become clearer.

## Open decisions, in priority order

| Question | Why it matters | When needed |
| --- | --- | --- |
| Personal tool, product for writers, or research tool? | Changes the core workflow and success criteria | Product brief refinement |
| Which writing contexts matter? | Determines the benchmark; detector targets are now confirmed | Before collecting samples |
| Which detector and features are enabled in the relevant Brightspace courses? | Identifies the actual vendor and report type behind the LMS | Before LMS evaluation |
| What detector access is already available? | Determines whether checks can be automated | Before integrations |
| Which permitted free allowances and existing local resources are available? | Determines what can run within the confirmed $0 budget | Before experiments |
| What quality tradeoffs are acceptable? | Defines useful results | Before held-out evaluation |
| What improvement, cost, and latency targets are required? | Prevents choosing success criteria after seeing results | Before held-out evaluation |
| Is sending drafts to external services acceptable? | Determines processing and retention constraints | Before submitting drafts |

## Sequence

1. **Refine the brief.** Confirm audience and writing context around the selected detector targets. Output: accepted product scope.
2. **Check access.** Verify official integrations, limits, costs, score definitions, and data handling. Output: provider comparison and a capped experiment budget.
3. **Prepare the benchmark.** Review sample provenance, create splits, and freeze the protocol. Output: dataset manifest and agreed acceptance targets.
4. **Run the feasibility experiment.** Compare originals, a basic rewrite, and a candidate method. Output: quality reviews and a reproducible results report.
5. **Make a go/no-go decision.** Proceed, collect more evidence, or revise the approach based on held-out results.
6. **Specify the application in detail.** Write UI, API, data, and operational specs around the validated workflow before building it.

## Next conversation

Establish existing GPTZero/Copyleaks accounts or API access, Turnitin/Brightspace role and report access, and the detector enabled in the relevant courses. Audience and writing context remain open. We do not need a custom machine-learning model or a full application to answer those questions.
