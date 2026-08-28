---
permalink: /
title: "Maxwell Woodfield"
excerpt: "Economist and statistician working in causal inference, survey microdata and applied machine learning."
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

<!--
REPLACES: _pages/about.md  in the Maxwell-Woodfield.github.io repository.
Rename this file to about.md on copy. Keep YOUR existing front matter if it differs from the block
above — permalink and redirect_from in particular must match what your site already uses, or you will
break existing inbound links. Everything below the front matter is safe to paste as-is.
Delete this comment block before committing.
-->

Economist and statistician working at the intersection of **causal inference**, **survey microdata**
and **applied machine learning**. My work runs from building the database upward: harmonizing raw
multi-wave survey sources into auditable relational schemas, then estimating treatment effects on top
of them under inference regimes strict enough to survive scrutiny.

I hold an **M.A. in Economics from Queen's University (GPA 4.0)** and a **B.A. in Economics and
Statistics from the University of British Columbia**. My research covers African development and
political economy, public finance and institutional trust, central bank digital currencies and
digital payments, and the robustness of published causal estimates under flexible machine-learning
estimators.

**Core areas** — Causal inference · Impact evaluation · Difference-in-differences · Instrumental
variables · Panel data and fixed effects · Double machine learning · Complex survey design and
weighting · Cluster-robust and small-cluster inference · Relational data engineering · Machine
learning and model validation · Python · R · SQL · Stata

---

## Education

### M.A., Economics — Queen's University
Kingston, Ontario · August 2025 – August 2026 · Degree conferred 1 August 2026 · **GPA 4.0**
Research supervisor: Professor Abhimanyu Gupta

Coursework: Quantitative Methods · Microeconomic Theory · Macroeconomic Theory · Money and Financial
Markets · Finance Theory · Reinforcement Learning (CISC) · Neural and Cognitive Computing (CISC)

### B.A., Double Major in Economics and Statistics — University of British Columbia
Vancouver, British Columbia · Graduated May 2025

- **Probability and inference** — Probability Theory · Statistical Inference for Data Science · Intermediate Statistics for Applications
- **Modelling and learning** — Advanced Econometrics · Methods for Statistical Learning · Statistical Modelling for Data Science · Finding Relationships in Data
- **Time series and stochastic processes** — Time Series and Forecasting · Stochastic Processes
- **Experimental design** — Design and Analysis of Experiments
- **Mathematics and optimization** — Linear Algebra · Applied Linear Algebra · Linear Programming

---

## Research

### Machine Learning and the Robustness of Causal Estimates: Evidence from Re-Estimated Studies in African Development
**M.A. Research Essay · Sole-authored · Queen's University · May – July 2026**
[Repository and replication code](https://github.com/Maxwell-Woodfield/Machine-Learning-and-the-Robustness-of-Causal-Estimates)

Influential findings in African development were estimated under parametric assumptions that modern
methods no longer require. This essay asks whether those findings survive when the assumptions are
relaxed.

- Re-estimated **three foundational papers** — Nunn and Wantchekon (2011) on slave-trade exposure and
  present-day trust, Depetris-Chauvin, Durante and Campante (2020) on football victories and national
  identity, and Weigel (2020) on a property-tax campaign and civic participation
- Applied **double machine learning** (partially linear, DML-IV, AIPW/DML-IRM, fixed-effect-residualized
  PLR) and **causal forests** with cross-fitting, using lasso, elastic net, gradient boosting, random
  forests and neural networks as nuisance learners
- Recovered both **average and heterogeneous treatment effects** without imposing restrictive
  functional form
- **The results split rather than uniformly confirming or overturning the literature.** Nunn's Table 3
  association and the Depetris-Chauvin/Durante/Campante estimates hold close to published values;
  Weigel's participation effects broadly survive while the evaluation-submission result weakens; and
  Nunn's instrumental-variables estimates prove fragile, with unstable score denominators
- Built on GPU-accelerated Python — RAPIDS (cuDF, cuML), CuPy, XGBoost and PyTorch on a CUDA runtime —
  to make repeated cross-fitting across multiple studies tractable

---

## Projects

### Trust in African Institutions: A Normalized Survey Database and Descriptive Panel
**August 2026** · [Repository, crosswalk and codebook citations](https://github.com/Maxwell-Woodfield/afrobarometer-institutional-trust)

Four Afrobarometer rounds, in which question codes, response scales and missing-value conventions all
shift between waves, integrated into a single queryable database with every mapping traceable to its
source.

- Integrated **Afrobarometer rounds 6–9 — 201,286 respondents across 42 African countries, 2.07 million
  raw answers, fielded 2014–2023** — into a **9-table normalized SQL database**
- Resolved cross-wave schema drift through an explicit crosswalk with **every mapping traced to a
  codebook page**, making the merge auditable by a third party
- Built survey-weighted country-round panels in SQL respecting the complex survey design (143 of 168
  possible country-round cells), then estimated two-way fixed-effects models in R with
  country-clustered standard errors
- **Found perceived government economic performance co-moving strongly with institutional trust —
  0.342 points on a 0–3 scale, roughly half a within-country standard deviation, bootstrap p = 0.001 —
  while perceived corruption shows a null relationship at −0.224 (p = 0.081–0.144)**, null under all
  three inference layers rather than under a single convenient specification
- Reported every estimate under **three inference layers**, with CR2 Satterthwaite degrees of freedom
  of 13–18, because the panel supports only 36 effective clusters. Findings are stated as descriptive
  associations, not causal effects

**Stack:** DuckDB (via R bindings) · SQL · R (haven, dplyr, tidyr, survey, fixest, clubSandwich, DBI, ggplot2)

---

### Mitigating Hallucination in Large Multimodal Models via Efficient Visual Attention Regularization
**March – April 2026** · [Repository](https://github.com/Maxwell-Woodfield/Mitigating-Hallucination-in-Large-Multimodal-Models-via-Efficient-Visual-Attention-Regularization)

Multimodal models often describe objects that are not in the image, falling back on language priors
instead of visual evidence. Full attention regularization corrects this but is expensive. This project
asks how much of the correction survives at a fraction of the cost.

- Implemented **three training-free attention and KV-cache interventions** for **LLaVA-1.5-7B** —
  Static Sink Biasing (Var-A), Targeted Layer and Head Hooking (Var-B), and Global KV-Cache Sink
  Dropping (Var-C)
- Benchmarked five configurations — unmitigated baseline, full VAR, and each simplified variant — on
  the **full MMVP set and randomized subsets of MME and POPE**, measuring accuracy jointly with
  **per-sample inference latency**
- **Established that only one of the three simplifications sits on the accuracy/latency frontier.**
  Static Sink Biasing captured half of full regularization's accuracy gain for roughly one percent of
  its cost; the other two bought at most +0.50 accuracy on MME for +87% latency
- **Reported the negative half as well: on POPE no simplified variant improved on the baseline.** Full
  VAR does work there — recall 85.0 → 97.5 — but at 5.3× baseline latency

| Variant | MME gain | MME latency | MMVP gain | MMVP latency | POPE |
|---|---|---|---|---|---|
| **Var-A — Static Sink Biasing** | **+1.50** | **+3.7%** | **+1.67** | **+11%** | no gain |
| Var-B — Targeted Layer/Head Hooking | +0.50 | +87% | 0.00 | +42% | no gain |
| Var-C — Global KV-Cache Sink Dropping | +0.50 | +88% | +2.00 | +53% | no gain |
| Full VAR (reference method) | +3.00 | +312% | +3.33 | +325% | recall 85.0 → 97.5 at 5.3× latency |

**Compute:** single NVIDIA L4 Tensor Core GPU (22.5 GB VRAM), Ubuntu 22.04 LTS, Google Colab.
VCD (Visual Contrastive Decoding) reproduced separately. Run scale was bounded by available compute,
so results characterize the proposed variants under those conditions rather than establishing general
performance gains.

---

### Adaptive Learning Rate Control Using Reinforcement Learning
**March – April 2026** · Co-authored with Jack Peterson, Mitchell Petingola and Syed Mekael Wasti
[Paper (PDF)](https://maxwell-woodfield.github.io/files/CISC_856_Final_Paper-compressed.pdf)

Learning-rate scheduling treated as an online sequential decision problem rather than a
hyperparameter to be tuned in advance.

- Trained a **Soft Actor-Critic** agent to control the learning rate during neural-network training
  over smoothed optimization signals
- Evaluated against tuned fixed and step-decay schedules on **LeNet-5 / Fashion-MNIST** and
  **ResNet-18 / CIFAR-10** across five runs each, with ablations on observation space, action scaling
  and reward design
- **Reported a negative result on the primary comparison:** the controller did not consistently
  outperform a tuned step-decay baseline
- **The transfer experiment was the positive finding.** A policy trained on ResNet-18 and applied to
  an unseen, larger ResNet-50 reached **78.89% ± 1.98 against the step-decay baseline's 73.32% ±
  4.26** — a 5.6-point gain at roughly half the variance

| Setting | Fixed LR | Step decay | SAC agent |
|---|---|---|---|
| LeNet-5 / Fashion-MNIST | 89.2% ± 0.2 | 89.4% ± 0.4 | 89.6% ± 0.7 |
| ResNet-18 / CIFAR-10 | 78.0% ± 1.3 | 78.8% ± 1.9 | 78.3% ± 2.3 |
| **Transfer:** ResNet-18 policy → ResNet-50 / CIFAR-10 | — | 73.32% ± 4.26 | **78.89% ± 1.98** |

**Stack:** PyTorch · Stable Baselines (SAC)

---

### Loan Approval Classification: A Comparative Study of Machine Learning Models
**October – November 2025** · [Report (PDF)](https://maxwell-woodfield.github.io/files/Loan_Approval_Classification.pdf)

Automated credit approval as a model-selection problem, where a false approval and a false decline
carry very different costs.

- Built and benchmarked four classifiers — logistic regression as baseline, Random Forest, XGBoost and
  a neural network — on **44,988 applicant records** of financial and demographic data
- Engineered the full pipeline: feature construction, outlier treatment, one-hot encoding, **SMOTE**
  class rebalancing for the imbalanced default outcome, and randomized hyperparameter search
- **The champion Random Forest reached 97.27% ROC AUC and 92.59% accuracy against the logistic
  baseline's 95.30% and 89.64%. The material gain was in precision — 87.76% versus 76.86% — at
  near-identical recall (77.45% vs 76.40%)**, which is the trade-off that matters when a false approval
  costs more than a false decline
- Compared models on held-out performance with threshold tuning against precision targets rather than
  in-sample fit

**Stack:** scikit-learn · XGBoost · imbalanced-learn · pandas · NumPy · Matplotlib · Seaborn
**Scope note:** no fairness or adverse-impact testing was performed across demographic features.

---

### CBDC Resilience and Real Economic Behavior: Causal Evidence from the DCash Shutdown
**Research proposal · November 2025** · [Proposal (PDF)](https://maxwell-woodfield.github.io/files/821proj.pdf)

An identification strategy for what a prolonged central-bank digital-currency outage does to economic
activity and to confidence in digital public money.

- Designed a difference-in-differences and instrumental-variables strategy exploiting **exposure
  heterogeneity and outage timing** in transaction-level and merchant-level DCash data
- Specified **double machine learning** for heterogeneous treatment effects across merchant and
  regional characteristics
- Framed around CBDC reliability, adoption sustainability, systemic risk and digital financial
  inclusion in small open economies

**Status: proposal. Not estimated.**

---

## Experience

### Project Assistant Leader — Chapman Learning Commons, University of British Columbia
Irving K. Barber Learning Centre · Vancouver, British Columbia · May 2023 – May 2025

- Analyzed several thousand free-text patron enquiries logged at a university service desk over
  multiple years, building a Python pipeline (pandas, sentence-transformers, HDBSCAN) that normalized
  inconsistent staff-entered text, deduplicated semantically equivalent questions, and clustered them
  into a validated **ten-category service taxonomy**
- Delivered a frequency-ranked question-and-answer reference guide identifying the **~10% of enquiry
  types accounting for roughly 70% of desk volume**, coordinating with subject-matter experts across
  departments to write verified responses for high-frequency gaps
- **Led a team of 15 student staff**, providing training, project oversight and feedback on content
  development

---

## Technical Skills

**Methods and research design** — Causal inference · Quasi-experimental design · Impact evaluation ·
Difference-in-differences · Instrumental variables · Fixed effects · Panel data methods · Randomized
experiment analysis (intent-to-treat) · Design of experiments · Complex survey data and weighting ·
Replication and re-estimation · Research design evaluation

**Econometrics and inference** — Double/debiased machine learning (PLR, IRM/AIPW, DML-IV) ·
Cross-fitting · Causal forests · Two-way fixed-effects estimation · Survey-weighted estimation ·
Cluster-robust and two-way clustered inference · Small-cluster inference (CR2, Satterthwaite degrees
of freedom) · Wild cluster bootstrap · Randomization inference · Multiple-testing adjustment ·
Weak-instrument and first-stage diagnostics · Heterogeneous treatment effects

**Statistical and machine-learning methods** — Regularized regression (lasso, elastic net) · Gradient
boosting · Random forests · Ensemble methods · Neural networks · Reinforcement learning (Soft
Actor-Critic) · Sentence embeddings · Density-based clustering (HDBSCAN) · Class imbalance handling
(SMOTE) · Cross-validation and out-of-fold model selection · Randomized hyperparameter search · Time
series and forecasting · Stochastic processes

**Data management and research data engineering** — Relational schema design · SQL (DuckDB) · Data
harmonization and crosswalk construction across survey waves · Missing-value and coding-scheme
reconciliation · Data validation and integrity checks · Merge auditing · Metadata and codebook
extraction

**Programming** — Python (pandas, NumPy, scikit-learn, XGBoost, SciPy, statsmodels, Matplotlib,
Seaborn, imbalanced-learn) · R (fixest, survey, clubSandwich, haven, dplyr, tidyr, DBI, duckdb,
ggplot2) · SQL · Stata

**Deep learning and GPU computing** — PyTorch · TensorFlow · Keras · Stable Baselines ·
sentence-transformers · RAPIDS (cuDF, cuML) · CuPy · CUDA

**Tools** — Git and GitHub · Jupyter and Google Colab · DuckDB · LaTeX · RStudio · VS Code

**Domain knowledge** — African development and political economy · Public finance and taxation ·
Institutional trust and governance · Central bank digital currencies and digital payments · Monetary
economics · Credit risk and consumer lending

---

## Contact

**Email:** [maxwell.woodfield@gmail.com](mailto:maxwell.woodfield@gmail.com)
**GitHub:** [github.com/Maxwell-Woodfield](https://github.com/Maxwell-Woodfield)
**LinkedIn:** [linkedin.com/in/m-w-9266503b5](https://www.linkedin.com/in/m-w-9266503b5/)

**Location:** Vancouver, British Columbia, Canada — open to relocation
**Work authorization:** Canadian citizen
**Languages:** English (native) · French (conversational)
