# Detector farm specifications

Status: Draft · Updated: 2026-09-23

Build this feature in small parts. The user requested paragraph-by-paragraph checks against the target commercial detectors and a dedicated `farm` specification folder. Here, “farm” means the coordinator that schedules detector checks and collects results; it does not imply locally hosted commercial detector models.

| Document | Purpose |
| --- | --- |
| [01-paragraph-checking.md](01-paragraph-checking.md) | First feature scope, processing rules, records, and implementation milestones |

## Confirmed direction

- Work on this feature incrementally, starting with paragraphs.
- Target GPTZero, Turnitin, and Copyleaks, subject to actual access.
- Keep the project within its confirmed $0 budget.
- The coordinator can be ordinary software; it does not need an LLM.
- This step produces specifications, not an implemented integration or a tested detector result.

## Requested access mechanism and feasibility

The user proposed incognito sessions, proxies, rotating IPs, and repeated resets of free checks. The stated “250 free characters” allowance has not been verified for a specific provider, product, or account. Do not encode that number as a provider limit.

That proposed mechanism is not an accepted implementation dependency. Session resets and new IPs do not establish renewed entitlement or unlimited compute. The existing [zero-budget research](../07-zero-budget-feasibility.md) records access and automation restrictions; account access remains unverified. This draft specifies bounded checks through supported access, explicit exhaustion states, and manual report import where suitable. It does not specify account cycling or quota-bypass automation.

Commercial detector availability is a dependency to establish, not an assumed capability. A local detector, mock, or another vendor cannot stand in for an unavailable target's result.

## Relationship to existing plans

This folder details the detector-checking component of the [system outline](../04-system-outline.md). The [evaluation plan](../03-evaluation-plan.md) still governs effectiveness claims. Paragraph checks are a new experiment granularity; they do not replace whole-document evaluation or establish whole-document outcomes.
