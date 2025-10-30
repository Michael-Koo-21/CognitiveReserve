# Cognitive Reserve in Alzheimer’s Disease: A Data-Driven Exploration

# Cognitive Reserve in Alzheimer’s Disease: Report

Author: Michael Koo  ·  Date: 2025-10-29  ·  Repository: CognitiveReserve

This page is a standalone report. You can skim the findings below without opening the notebook; the code remains available for transparency.

---

## Executive summary (TL;DR)

- Goal: explore how cognitive reserve (CR) proxies—especially education—relate to cognition and Alzheimer’s disease status in an open dataset.
- Approach: clean and explore the cohort; engineer simple CR proxies; fit interpretable baseline models; visualize relationships and diagnostics.
- Headline patterns
  - Cognition tends to decline with age; higher education is associated with better cognitive scores in this cohort.
  - Education appears to buffer age-related decline (consistent with CR theory), though effects vary by specification.
  - Pairwise correlations are generally modest; relationships are multi-factor and require modeling to tease apart.
- Caveats: observational data; proxies for CR are imperfect; do not infer causality.

---

## Data access and cohort

- Source: Kaggle dataset “Alzheimer’s Disease Dataset”
  - URL: https://www.kaggle.com/datasets/rabieelkharoua/alzheimers-disease-dataset
  - This repository does NOT include the raw CSV. After downloading, place it at the project root as `alzheimers_disease_data.csv` (or update the path in the notebook).
- Typical variables: age, sex, education (years/levels), cognitive assessments (e.g., MMSE), ADL/functional assessments, and diagnosis indicators.
- Outcome focus: cognition-related measures (e.g., MMSE). Education is used as a practical proxy for cognitive reserve.

---

## What to look at in the figures

Below are curated figures exported from the notebook with short takeaways.

<p align="center">
   <img src="figures/overview.png" alt="Project overview figure" width="70%"/>
   <br/>
   <em>Figure 1. Study flow and components at a glance.</em>
   <br/>
</p>

<p align="center">
   <img src="figures/eda_distributions.png" alt="Distributions of Age, MMSE, Education, Diagnosis, ADL, Functional Assessment" width="46%"/>
   <img src="figures/correlation_heatmap.png" alt="Correlation matrix across key variables with MMSE" width="46%"/>
   <br/>
   <em>Figures 2–3. Cohort context. Left: key variable distributions. Right: modest pairwise correlations, suggesting multi-factor drivers.</em>
</p>

<p align="center">
   <img src="figures/age_mmse_by_education.png" alt="Age vs MMSE by education levels" width="46%"/>
   <img src="figures/diagnosis_rate_by_age_education.png" alt="Diagnosis rates by age bins and education" width="46%"/>
   <br/>
   <em>Figures 4–5. Left: cognition tends to decline with age; higher education levels align with higher scores. Right: diagnosis rates rise with age and differ by education.</em>
</p>

<p align="center">
   <img src="figures/mmse_regression_diagnostics.png" alt="Linear regression diagnostics" width="46%"/>
   <img src="figures/simple_slopes_age_mmse_education.png" alt="Simple slopes: Age × Education on MMSE" width="46%"/>
   <br/>
   <em>Figures 6–7. Model sanity checks and interaction. Diagnostics are acceptable for a baseline. Simple slopes suggest education may buffer age-related decline.</em>
</p>

---

## Background (why cognitive reserve?)

Cognitive reserve (CR) explains why some people maintain better cognition than expected given similar brain pathology. In practice, researchers use proxies—like education, occupational complexity, or cognitively stimulating activities—to approximate CR. Here, we primarily use education for its availability and interpretability.

References: Stern (2009); Stern et al. (2020). See `litReview.md` for a short literature survey.

---

## Methods at a glance

1. Data hygiene and EDA: missingness checks, outliers, distributions, and bivariate plots.
2. CR proxies: education-driven proxy variables; simple alternative specifications tested.
3. Modeling: baseline linear regressions and simple tree-based variants; cross-validated metrics; diagnostics (residuals, QQ, actual vs. predicted).
4. Interpretation: emphasize direction/magnitude patterns and robustness cues rather than over-precise estimates.

---

## Key findings (narrative)

- Age vs. cognition: a negative association emerges across specifications.
- Education and cognition: higher education levels align with higher cognitive scores.
- Buffering patterns: interaction views suggest education may attenuate age-related decline (consistent with CR theory), though effect sizes vary.
- Cohort structure matters: distributions and modest correlations imply multi-factor interactions.
- Modeling takeaway: simple, interpretable models capture broad patterns but leave room for richer structures and confounder control.

Please treat these as exploratory patterns specific to this dataset and preprocessing.

---

## Limitations and considerations

- Proxies for CR are imperfect; education captures only part of the construct.
- Observational design: confounding and selection bias are possible; results are not causal.
- Measurement constraints: single-timepoint, limited variable granularity, and sample composition shape estimates.
- External validity is untested here; replication across cohorts is encouraged.

---

## What’s next

- Broaden CR proxies (occupational complexity, bilingualism, cognitive engagement indices).
- Longitudinal modeling for change over time and moderation effects.
- Stronger confound control and causal designs when feasible.
- Model interpretability extensions (e.g., partial dependence, SHAP) with careful validation.

---

## Appendix A — Reproduce or extend the analysis

- Notebook: `cognitive_reserve_analysis.ipynb`
- Data: download from Kaggle and place `alzheimers_disease_data.csv` at the repository root (or update the path in the notebook).

Environment setup (macOS/Linux):

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Open the notebook:

```bash
jupyter lab  # or: jupyter notebook
```

Export visuals (optional):

```bash
jupyter nbconvert --to markdown cognitive_reserve_analysis.ipynb --output tmp_nb
```

Copy curated images (optional):

```bash
cp tmp_nb_files/tmp_nb_11_0.png figures/eda_distributions.png
cp tmp_nb_files/tmp_nb_14_1.png figures/correlation_heatmap.png
cp tmp_nb_files/tmp_nb_17_0.png figures/age_mmse_by_education.png
cp tmp_nb_files/tmp_nb_18_0.png figures/diagnosis_rate_by_age_education.png
cp tmp_nb_files/tmp_nb_23_0.png figures/mmse_regression_diagnostics.png
cp tmp_nb_files/tmp_nb_34_0.png figures/simple_slopes_age_mmse_education.png
```

Export to PDF (optional):

```bash
jupyter nbconvert --to pdf cognitive_reserve_analysis.ipynb
```

---

Curated and analyzed by Michael Koo. Feedback and collaboration are welcome.