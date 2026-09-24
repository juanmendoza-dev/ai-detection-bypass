# Detector farm specifications

Status: Draft · Updated: 2026-09-23

Build this feature in small parts. The user requested paragraph-by-paragraph checks against commercial detectors and a dedicated `farm` specification folder. The user subsequently clarified that “farm” specifically means repeated free-account creation, scanning, result collection, and IP rotation across detector providers. It does not mean locally hosted commercial detector models. This records requested product intent, not validated access or feasibility.

| Document | Purpose |
| --- | --- |
| [01-paragraph-checking.md](01-paragraph-checking.md) | Previously proposed quota-aware alternative; shared paragraph and result requirements |

## Confirmed direction

- Work on this feature incrementally, starting with paragraphs.
- Target GPTZero, Turnitin, and Copyleaks, subject to actual access.
- Keep the project within its confirmed $0 budget.
- The coordinator can be ordinary software; it does not need an LLM.
- This step produces specifications, not an implemented integration or a tested detector result.

## Requested access mechanism and feasibility

The requested farm would:

1. Receive text from the parent project, initially at paragraph granularity.
2. Create a free account with a target AI detector provider, for example GPTZero.
3. Submit the text and obtain the detector's result.
4. Return and persist that result in the parent project, linked to the exact input and provider.
5. Repeat with newly created accounts, using IP rotation as part of the requested mechanism.
6. Extend the same collection workflow to multiple AI detector providers.

“Providers” here means detector services, not text-generation model providers. Repeated account creation is central to the user's requested design, not an incidental implementation choice. The user has not accepted the quota-aware queue as a replacement for this mechanism.

Earlier requests also mentioned incognito sessions and proxies. The stated “250 free characters” allowance has not been verified for a specific provider, product, or account. Do not encode that number as a provider limit.

Feasibility remains unresolved: new accounts, session resets, and new IPs do not establish renewed entitlement or unlimited compute. The existing [zero-budget research](../07-zero-budget-feasibility.md) records access and automation restrictions; account access remains unverified. This document captures the requested lifecycle but does not provide an account-cycling or quota-bypass implementation procedure.

The bounded queue, exhaustion states, and manual import in `01-paragraph-checking.md` were an assistant-proposed alternative. They must not be presented to an implementer as accepted substitutes for the user's requested farm. Paragraph identity, raw-result preservation, and provider-specific score semantics remain useful shared requirements.

Commercial detector availability is a dependency to establish, not an assumed capability. A local detector, mock, or another vendor cannot stand in for an unavailable target's result.

## Relationship to existing plans

This folder details the detector-checking component of the [system outline](../04-system-outline.md). The [evaluation plan](../03-evaluation-plan.md) still governs effectiveness claims. Paragraph checks are a new experiment granularity; they do not replace whole-document evaluation or establish whole-document outcomes.
