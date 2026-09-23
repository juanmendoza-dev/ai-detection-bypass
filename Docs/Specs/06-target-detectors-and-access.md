# Target detectors and access

Status: Draft; target list confirmed by user · Sources checked: 2026-09-23

## Confirmed targets

GPTZero, Turnitin, and Copyleaks are the priority detector vendors. D2L Brightspace is the relevant learning management system (LMS). The user supplied [GPTZero](https://gptzero.me/), [Turnitin](https://www.turnitin.com/), and [Copyleaks' Brightspace integration](https://copyleaks.com/learning-management-systems/brightspace-plagiarism-checker).

No ranking among the three detectors has been specified. The implementation order below is a proposal based on access, not an importance ranking.

## Platform versus detector

Brightspace hosts course and assignment workflows. D2L documents a [Turnitin integration](https://community.d2l.com/brightspace/kb/articles/4997-assignments-and-turnitin), and Copyleaks advertises a [Brightspace plugin with plagiarism and AI detection](https://copyleaks.com/learning-management-systems/brightspace-plagiarism-checker). Treat Brightspace as an integration context, not a fourth independent detector in this benchmark.

We do not yet know which provider, features, or settings are enabled in the user's courses. A Brightspace login alone does not establish access to either vendor's AI report.

## Provider comparison

| Target | Verified public information | Access still to establish | Proposed evaluation path |
| --- | --- | --- | --- |
| GPTZero | An official API accepts text/files and returns document, paragraph, and sentence-level probabilities [1] | API credentials, plan, limits, costs, retention, and exact response semantics | Candidate for the first automated adapter |
| Copyleaks | Official AI Text Detection API documentation exists [2]; its Brightspace plugin advertises both AI and plagiarism detection [3] | API entitlement, costs, limits, retention, and which features the institution enables | Candidate for a second adapter; record standalone API and LMS checks separately |
| Turnitin | Individual Turnitin licenses are not sold [4]; AI reports have their own eligibility requirements [5] | Institutional access, AI feature entitlement, report visibility, and an approved test workflow; programmatic AI-report access is unverified | Use authorized reports or an institutional test environment if available; otherwise mark untested |
| D2L Brightspace | Integrates assignment workflows with Turnitin [6]; Copyleaks offers a plugin [3] | Actual course integration, enabled features, user role, and report availability | Record LMS context alongside the actual detector; do not invent a Brightspace AI score |

The existence of an API does not establish account access or identical behavior between API, website, and LMS products. Verify those relationships through documentation or paired observations before pooling results.

## AI detection versus similarity

AI detection estimates whether text has characteristics associated with generated writing. Similarity checking identifies overlaps with source material. Keep them as separate result types; a similarity percentage cannot substitute for an AI result. D2L's Turnitin documentation describes Similarity Reports, while Turnitin documents its AI Writing Report separately. [5][6]

For Turnitin, the AI percentage refers to qualifying prose. Its guide requires at least 300 words of long-form prose and suppresses numerical results from 1–19% with an asterisk. Preserve that asterisk as a non-numeric result; it is neither zero nor an error. Check all current file, language, and length requirements before running samples. [5]

D2L support describes the Turnitin AI indicator as instructor-only in its published answer. Confirm current visibility for the actual account; a student-visible similarity report does not establish AI-report access. [7]

## Proposed test setup

1. Establish GPTZero and Copyleaks access and a budget before selecting the initial adapters.
2. Establish a Turnitin workflow separately. Do not substitute another vendor's result for a missing Turnitin check.
3. Use eligible long-form prose for comparisons that include Turnitin. Keep shorter texts as a separate eligibility group and do not pad them just to obtain a score.
4. Record vendor, product, access surface (API, website, or LMS), integration, enabled features, version if exposed, date, and report type.
5. If all three vendors are accessible, consider reserving one from method selection for transfer testing. Decide which before the experiment.
6. For LMS experiments, use an agreed test assignment and establish submission storage/indexing settings first. Do not use real graded submissions as an experiment harness.

No accounts have been accessed, documents submitted, plans purchased, or integrations implemented. Access checks are the next dependency; budget and provider data handling remain unresolved.

## Sources

1. [GPTZero: What is the GPTZero API?](https://support.gptzero.me/articles/7675217351-what-is-an-api-what-is-the-gptzero-api)
2. [Copyleaks: AI Text Detection API](https://docs.copyleaks.com/concepts/products/ai-text-detection-api/)
3. [Copyleaks: Brightspace plugin](https://copyleaks.com/learning-management-systems/brightspace-plagiarism-checker)
4. [Turnitin: Individual subscriptions and licenses](https://helpcenter.turnitin.com/hc/en-us/articles/27974736791565-How-can-I-buy-a-Turnitin-subscription-license-for-myself)
5. [Turnitin: Using the AI Writing Report](https://guides.turnitin.com/hc/en-us/articles/22774058814093-Using-the-AI-Writing-Report)
6. [D2L: Assignments and Turnitin](https://community.d2l.com/brightspace/kb/articles/4997-assignments-and-turnitin)
7. [D2L support: Can students see AI reports with Turnitin?](https://community.d2l.com/brightspace/discussion/comment/16570)
