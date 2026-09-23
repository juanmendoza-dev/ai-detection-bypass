# Zero-budget feasibility

Status: Draft; $0 budget confirmed by user · Research checked: 2026-09-23

## Question

Does creating a free GPTZero or Copyleaks account unlock its best detector, and can account creation/deletion or fresh instances support ongoing automated testing at no cost?

## Findings

| Question | Finding | Confidence and limit |
| --- | --- | --- |
| Does GPTZero free signup unlock a better model than guest access? | Not established. GPTZero advertises Advanced Scan separately and associates it with advanced accuracy, while its support article describes general free/paid differences mainly as usage limits and educator-specific data/thresholds [1][2] | Neither source establishes that every new free account receives the strongest model. Current Advanced Scan entitlement and model identity remain unverified |
| Does Copyleaks free signup unlock a better model? | Its page describes additional credits and richer reports after signup, but does not explicitly document a different detector model [3] | More features are established as a vendor offer; a model upgrade or equivalence with enterprise/LMS detection is not |
| Can the project rely on repeated account creation/deletion? | No supported recurring-free entitlement was found. GPTZero prohibits automated account creation and access-restriction bypass; Copyleaks restricts unauthorized automation and circumvention of usage rules [4][5] | Not a viable supported test dependency. Deletion is not documented as resetting trial eligibility |
| Would a fresh browser or server instance solve access limits? | No entitlement change is documented | A new runtime is not evidence of new quota or access to model weights. Self-hosted vendor detector instances remain unverified |

GPTZero's support article does not specifically settle the guest-versus-registered comparison. The earlier free/paid summary must not be read as proof that all scan modes use identical models. [1][2]

The public GPTZero pricing page did not expose a complete free-plan breakdown in the retrieved text. No browser was available to inspect its rendered interface. No account was created or inspected, and no live scan was run. Exact advanced-scan allowance and renewal behavior require direct account evidence or vendor clarification. Do not promote third-party quota descriptions to confirmed requirements.

Copyleaks' detector page advertises guest scans, while its terms say use of the services requires an account. Record this documentation inconsistency and verify actual account access instead of assuming anonymous automated access. [3][5]

## Automation and project use

GPTZero's terms explicitly cover automated account creation and automated site access. An official API offer must be evaluated under its applicable permissions; it is not blanket permission to automate the website. [4]

Copyleaks' general restrictions include unauthorized automated access, circumvention of usage rules, competing/similar products, and using service content to develop, train, or improve other ML/AI models, subject to stated exceptions or express written authorization. Public access alone does not establish permission for a detector-feedback optimization project. Confirm the applicable scope before making Copyleaks a development dependency. [5]

These are concrete service constraints found during feasibility research, not a claim that browser automation is technically impossible. No account-cycling bot is proposed for implementation.

## Proposed $0 plan

1. Build the local experiment runner, result schema, quality-review workflow, and report import/export without requiring a paid service.
2. Use mocks only to verify software behavior. Exclude them from every detector-performance metric.
3. Treat a single free account per provider as a possible source of limited checks, subject to verified entitlement and permitted project use. Record plan, scan mode, quota, renewal date if documented, and API versus website access.
4. Stop checks when allowance is exhausted. Do not make deletion/re-registration or fresh instances a quota-renewal mechanism.
5. Use local models only after checking available hardware and licenses. These could support writing experiments or separate detector baselines; they do not reproduce GPTZero, Copyleaks, or Turnitin results.
6. Consider requesting research access only if the vendor supports the proposed use; no free grant is assumed and no outreach is authorized yet.

The proposed 60-document pilot with three text conditions and two detectors can require 360 real checks before retries. Current free quotas do not establish that this is achievable at $0. A handful of free checks can establish access and report format, but not validate broad effectiveness.

## Budget requirements

- External spend is $0 across detection, rewriting, compute, hosting, and storage.
- No paid plans, metered paid calls, or payment-backed auto-renewing trials.
- Use existing resources and confirmed free allowances; record their limits.
- Keep the commercial-detector evaluation optional until adequate permitted access exists.

## Sources

1. [GPTZero: Free versus paid plans](https://support.gptzero.me/articles/1272562776-what-is-the-difference-between-the-free-and-paid-for-plans)
2. [GPTZero: Advanced Scan product descriptions](https://gptzero.me/)
3. [Copyleaks: AI detector and signup benefits](https://copyleaks.com/ai-detector)
4. [GPTZero: Terms of Use, user representations and prohibited activities](https://gptzero.me/terms-of-use.html)
5. [Copyleaks: Terms of Use, site users and restrictions](https://copyleaks.com/termsofuse)
