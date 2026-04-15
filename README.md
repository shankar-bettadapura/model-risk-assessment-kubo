# Model Risk Assessment: BitNet + TurboQuant Ablation Study
### Kubo Technologies

**Frameworks:** NIST AI Risk Management Framework (AI RMF 1.0) | ISO/IEC 42001:2023
**Document Type:** Consulting-style model risk assessment
**Status:** Complete

> **Portfolio Note:** This report applies AI governance methodology to a real machine learning ablation study conducted for Kubo Technologies. The assessor trained the baseline model, implemented both compression variants, and produced the quantitative results that form the evidence base for this assessment. All governance findings and recommendations are analytical outputs produced for portfolio demonstration purposes.

---

## Overview

This project bridges hands-on ML work and GRC governance methodology. A 25M parameter GPT-style language model was trained from scratch on an NVIDIA RTX 3070, then evaluated under two compression techniques: BitNet ternary weight quantization and TurboQuant KV cache compression.

The model risk assessment evaluates whether the ablation study's findings provide a sufficient evidence base for a production deployment decision, and documents the governance gaps that prevent that decision from being made on objective grounds.

**The assessment concluded that neither technique is ready for production deployment without three specific governance gaps being resolved.**

---

## Technical Results

| Phase | Train Loss | Val Loss | Perplexity |
|---|---|---|---|
| Phase 1 — Baseline | 1.4650 | 1.4446 | 4.24 |
| Phase 2 — BitNet | 1.8018 | 1.7799 | 5.93 (+39%) |

**TurboQuant perplexity delta:** +0.27 to +0.56 across tested context lengths (3–5% degradation)

**TurboQuant memory benefit:** Not demonstrated at tested context lengths. Hardware limited evaluation to 512-token maximum. TurboQuant's primary benefit materializes above 4,096 tokens.

---

## Frameworks Applied

### NIST AI Risk Management Framework (AI RMF 1.0)
Used to structure the assessment across four core functions: GOVERN, MAP, MEASURE, and MANAGE. Subcategory references provided for each risk and finding.

### ISO/IEC 42001:2023
Used as the compliance anchor, mapping each finding to mandatory clause requirements and Annex A controls. Key clauses in scope: Cl. 5 (Leadership), Cl. 6.1.2 (Risk Assessment), Cl. 8 (Operation), Cl. 9 (Performance Evaluation).

---

## Key Findings

| ID | Finding | Severity |
|---|---|---|
| F-01 | No performance acceptance threshold defined. BitNet's 39% perplexity degradation has no documented criterion against which to evaluate acceptability. | Critical |
| F-02 | TurboQuant memory benefit not demonstrated. Hardware constrained evaluation to 512 tokens; primary benefit requires 4,096+ token context. | Critical |
| F-03 | No production lifecycle controls. No monitoring framework, alerting thresholds, or rollback procedure defined for compressed model variants. | High |

**Overall Risk Posture: CRITICAL — Deployment not recommended without remediation of all three findings.**

---

## Risk Register Summary

8 risks identified across GOVERN, MAP, MEASURE, and MANAGE functions:

- 2 Critical risks (no acceptance threshold, TurboQuant benefit untested)
- 4 High risks (dataset representativeness, no monitoring, no rollback, measurement gaps)
- 2 Medium risks (no model owner defined, scale extrapolation unvalidated)

Full risk register with likelihood/impact scoring, framework references, and recommended controls is in the assessment report.

---

## Remediation Roadmap

| Phase | Timeframe | Focus |
|---|---|---|
| Pre-Decision Gate | Before any deployment decision | Define performance acceptance threshold; assign model owner role |
| Pre-Deployment Gate | Before any compressed model goes live | Evaluate TurboQuant at production context lengths; re-evaluate on production-domain data; expand evaluation to adversarial robustness, latency, and fairness |
| Go-Live Gate | Before production traffic is served | Implement production monitoring; define and test rollback procedure |

---

## Deliverable

The full assessment report is available in this repository:
📄 [`Model_Risk_Assessment_Kubo.docx`](./Model_Risk_Assessment_Kubo.docx)

---

## Skills Demonstrated

- ML model training and compression technique implementation (BitNet, TurboQuant)
- Risk identification and assessment grounded in quantitative experimental results
- NIST AI RMF 1.0 subcategory mapping
- ISO/IEC 42001:2023 clause and Annex A control mapping
- Model lifecycle risk assessment
- Production deployment decision governance

---

## Related Projects

This is the second in a two-part AI governance portfolio series.

| Project | Description | Link |
|---|---|---|
| Part 1: NovaSphere Technologies | Full AI governance assessment for a fictional SaaS company | [ai-governance-risk-assessment](#) |
| Part 2: Kubo Technologies | Model risk assessment of a real ML ablation study | This repo |

---

## About

This project was developed as part of a cybersecurity and AI governance portfolio targeting IT GRC Analyst roles. Background includes U.S. Army All-Source Intelligence Analysis, GRC consulting, and an M.S. in Cybersecurity Studies.

**Certifications:** CompTIA Security+ | CISA (in progress) | CRISC (in progress) | ISO 42001 (in progress)

🔗 [www.linkedin.com/in/shankar-bettadapura](#) | 🔗 [[Substack](https://shankarbettadapura.substack.com)](#)
