# Detector research

Status: Draft · Sources checked: 2026-09-23

## How detection works

There is no single detector algorithm to reverse. Relevant method families include:

| Family | Basic mechanism | Consequence for this project |
| --- | --- | --- |
| Trained classifiers | Learn differences between labeled human and generated examples | Evaluate on writing outside the development set; training coverage matters |
| Model probability methods | Examine how a language model scores the text and variations of it | A simple vocabulary rule cannot represent the entire method |
| Watermark detection | Looks for a statistical signal intentionally inserted during generation | A distinct mechanism; do not assume every generator embeds a watermark |

An example of a trained classifier was [OpenAI's retired text classifier](https://openai.com/index/new-ai-classifier-for-indicating-ai-written-text/). Its July 2023 withdrawal for low accuracy is historical evidence, not a measurement of today's commercial detectors.

[DetectGPT (2023)](https://arxiv.org/abs/2301.11305) compares model log probabilities for a passage and perturbed versions to estimate a curvature-based signal. It illustrates why “perplexity” alone is an incomplete description of detector technology.

[Kirchenbauer et al. (2023)](https://arxiv.org/abs/2301.10226) describe a generation-time watermark that preferentially samples selected tokens and a statistical test for the resulting pattern. This research does not establish which current products use watermarks.

## Findings that should shape the experiment

- [RAID (ACL 2024)](https://aclanthology.org/2024.acl-long.674/) evaluates detectors across generators, domains, and perturbations and reports robustness limitations. Its implication for us is to test varied documents and unseen conditions, rather than choose a few favorable examples.
- [Sadasivan et al.](https://arxiv.org/abs/2303.11156) show reduced detection under paraphrasing in their experiments and analyze limits as human and machine text distributions converge. This supports testing rewriting; it does not guarantee success against every current detector.
- [Liang et al. (2023)](https://arxiv.org/abs/2304.02819) found false-positive disparities for non-native English writing in the detectors and samples studied. Include diverse human-written controls; do not generalize the historical rates to all products today.
- [Turnitin's current report guide](https://guides.turnitin.com/hc/en-us/articles/22774058814093-Using-the-AI-Writing-Report) says its percentage represents qualifying text flagged by the model. It suppresses numerical results from 1–19% because of false-positive concerns and describes detection of AI text modified with paraphraser or bypasser tools. These are vendor descriptions, not independent validation.

## Interpretation

A detector score can mean a document-level estimate, a share of flagged text, or another vendor-specific measure. Never average raw scores across vendors or assume “80%” has the same meaning everywhere. A score change does not change the known origin of the text.

Working inference: start with black-box evaluation of accessible detectors and quality-preserving rewriting. We do not need to reproduce a proprietary detector's architecture before testing feasibility.

## Research still needed

- Choose the detectors that matter to the intended user.
- Verify official access, score semantics, supported languages, length limits, pricing, retention, and automation terms for each candidate.
- Record model versions where exposed; otherwise record the date and that the version is unknown.
- Check more recent independent evaluations for the chosen detectors. The foundational papers above are not a 2026 product ranking.
- Inspect benchmark licenses and provenance before downloading or reusing samples.

No commercial detector integration, pricing, or performance claim has been validated for this project yet.
