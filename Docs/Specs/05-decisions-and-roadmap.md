# Decisions and roadmap

Status: Draft · Updated: 2026-09-23

## Confirmed instructions

| Decision | Basis |
| --- | --- |
| Specifications live in `Docs/Specs` | User request |
| Begin with planning and research | User request |
| Explore an AI text bypasser | User's stated product idea |

## Proposed defaults

English prose; personal draft editing as the provisional audience; an existing language model; an evaluation harness before a web interface; no custom training initially. These defaults keep the first experiment small and can change as requirements become clearer.

## Open decisions, in priority order

| Question | Why it matters | When needed |
| --- | --- | --- |
| Personal tool, product for writers, or research tool? | Changes the core workflow and success criteria | Product brief refinement |
| Which writing contexts and detectors matter? | Determines the benchmark and provider research | Before collecting samples |
| What detector access is already available? | Determines whether checks can be automated | Before integrations |
| What is the experiment budget? | Bounds documents, providers, and retries | Before paid requests |
| What quality tradeoffs are acceptable? | Defines useful results | Before held-out evaluation |
| What improvement, cost, and latency targets are required? | Prevents choosing success criteria after seeing results | Before held-out evaluation |
| Is sending drafts to external services acceptable? | Determines processing and retention constraints | Before submitting drafts |

## Sequence

1. **Refine the brief.** Confirm audience, writing context, and target detectors. Output: accepted product scope.
2. **Check access.** Verify official integrations, limits, costs, score definitions, and data handling. Output: provider comparison and a capped experiment budget.
3. **Prepare the benchmark.** Review sample provenance, create splits, and freeze the protocol. Output: dataset manifest and agreed acceptance targets.
4. **Run the feasibility experiment.** Compare originals, a basic rewrite, and a candidate method. Output: quality reviews and a reproducible results report.
5. **Make a go/no-go decision.** Proceed, collect more evidence, or revise the approach based on held-out results.
6. **Specify the application in detail.** Write UI, API, data, and operational specs around the validated workflow before building it.

## Next conversation

Start by deciding who this is for and which detectors matter. We do not need a custom machine-learning model or a full application to answer those questions.
