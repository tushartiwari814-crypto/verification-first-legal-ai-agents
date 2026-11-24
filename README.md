# A Verification-First Reference Architecture for AI Legal Document Review Agents

[![Conference](https://img.shields.io/badge/Submission-Confluence'27%20(IEEE%20%2371526)-blue)](https://cmt3.research.microsoft.com/Confluence2027)
[![Review Status](https://img.shields.io/badge/Review-Double--Blind%20Anonymous-lightgrey)](#double-blind-anonymity-notice)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> **Double-Blind Anonymity Notice:** This repository accompanies Paper ID **#1560** submitted to the *2027 17th International Conference on Cloud Computing, Data Science & Engineering (Confluence'27)*, Amity University, Noida. Author identities and affiliations have been withheld for double-blind peer review.

---

## Overview

AI agents powered by Large Language Models (LLMs), Retrieval-Augmented Generation (RAG), and multi-agent frameworks are increasingly deployed for legal document review, yet reliability evidence remains scattered across system papers, empirical benchmarks, court sanction orders, and ethics opinions.

This repository hosts the anonymized manuscript, secondary quantitative synthesis data, analytical reproduction scripts, and experimental evaluation specifications for the **Verification-First Reference Architecture (VFRA)**.

### Key Contributions
1. **Seven-Item Failure-Mode Taxonomy (`F1`–`F7`):** Synthesizes quantitative findings from **26 open-access sources** (2018–2026) covering retrieval granularity bias, context contamination, cost-accuracy gaps, multi-agent coordination drift, under-specified queries, fabricated authorities, and extraction ceilings.
2. **Quantitative Failure-Mode Analyses:**
   * **Noise-Degradation Linear Fit (`F2`):** Recomputes ordinary least-squares slopes for charge-prediction accuracy ($\text{Accuracy} = 41.3 - 2.05k\text{ pp}$) and mean absolute error ($\text{Error} = 24.6 + 1.15k\text{ months}$) under irrelevant document injection ($k \in \{0, 2, 4, 6\}$).
   * **Probabilistic Citation-Fabrication Risk Model (`F6`):** Evaluates the document-level residual risk $R(p, n, r) = 1 - [1 - p(1 - r)]^n$ across baseline hallucination rates ($p \in \{3\%, 13\%\}$), citation counts ($n \in \{10, 20\}$), and independent verifier recall ($r \in \{0, 0.90, 0.95, 0.99\}$).
3. **Verification-First Reference Architecture (`R1`–`R7`) & Evaluation Protocol:** Maps seven technical controls to the failure modes they mitigate and the professional duties established under **ABA Formal Opinion 512** (Model Rules 1.1, 1.4, 1.5, 1.6, 3.3, 5.1, 5.3, and 8.4(c)), paired with falsifiable hypotheses (`H1`–`H3`).

---

## VFRA Requirements Mapping

| ID | Architectural Requirement | Target Failure Mode | ABA Model Rule |
| :--- | :--- | :--- | :--- |
| **R1** | Multi-viewpoint query restatement & clarification prior to retrieval | `F5` Under-specified queries | Rule 1.1 |
| **R2** | Separate indexing of statutes/rules vs. case facts (Hierarchical retrieval) | `F1` Granularity bias | Rule 1.1 |
| **R3** | Strict relevance gating & context item cap | `F2` Context contamination | Rule 1.1 |
| **R4** | Size-aware aggregation (voting for ~8B models; bounded debate for ≥30B) | `F3` Cost-accuracy gap, `F4` Coordination failure | Rules 5.1, 5.3 |
| **R5** | Independent primary-source citation verifier with blocking gate | `F6` Fabricated authority | Rules 3.3, 8.4(c) |
| **R6** | Mandatory human-in-the-loop review with full audit & time logging | `F7` Extraction ceiling | Rules 1.1, 1.4, 1.5, 5.1 |
| **R7** | Confidential client-data isolation across all pipeline stages | Deployment constraint | Rule 1.6 |

---

## Repository Structure

```text
├── paper/
│   └── Confluence2027_IEEE_paper_anonymous.pdf   # Anonymous IEEE conference manuscript
├── data/
│   └── synthesized_sources_26.csv                # Quantitative data extracted from the 26 reviewed sources
├── analysis/
│   ├── noise_degradation_fit.py                  # Reproduces Section IV-A OLS regressions
│   └── citation_fabrication_risk.py              # Reproduces Section IV-C Table III probabilities
├── architecture/
│   └── vfra_evaluation_protocol.md               # Experimental design for Hypotheses H1–H3
├── LICENSE
└── README.md
