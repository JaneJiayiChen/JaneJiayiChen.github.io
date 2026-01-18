---
layout: single
title: "Mandibular MRONJ Imaging, Clinical Factors, and Surgical Outcomes (Study 1-2)"
permalink: /projects/mronj-imaging-study1/
author_profile: true
---

**Language:** English | [中文](/projects/mronj-imaging-study1-zh/)

## Background and Significance
MRONJ causes chronic infection, pain, and impaired function, and may progress to pathologic fracture.
Imaging is essential for staging, defining resection margins, and anticipating reconstruction needs.
We therefore ask two practical questions:
1) Do imaging differences map to specific clinical factors?
2) Can imaging + clinical features support surgical prognosis stratification?

## Study Design and Data
- **Design**: Retrospective cohort, 2015.01–2024.05, Peking University School and Hospital of Stomatology.
- **Inclusion**: Mandibular MRONJ, AAOMS stage 2–3; panoramic radiograph + spiral CT pre‑op; ≥6 months follow‑up.
- **Sample**: N=186; male 40.9%; mean age 64±9.73.
- **Imaging variables**: periosteal reaction, sequestrum separation, lesion density (destructive/sclerotic/mixed).
- **Clinical variables**: age, sex, primary disease grouping, MRONJ stage, medication type/duration, symptom‑to‑admission time, pre‑op dental treatment, labs.

## Variable Definitions and Handling
- **Imaging definitions**: lesion density reflects structural stage; sequestrum indicates necrotic bone separation; periosteal reaction reflects inflammatory/repair response.
- **Lab variables**: hemoglobin, albumin, calcium, glucose are retained as discrete normal/abnormal indicators.
- **Lab derivation**: if discrete columns are empty, indicators are derived from numeric values:
  - Hb ≥115 g/L, Albumin ≥40 g/L, Calcium ≥2.15 mmol/L, Glucose 4.85–20 mmol/L.
  - Adjust thresholds in `project/study1_config.py` / `project/study2_config.py` as needed.

## Statistical Approach
- Descriptive statistics: mean±SD or median[IQR].
- Association tests: chi‑square for categorical; t‑test or Mann–Whitney U for continuous.
- Multivariable models: binary Logistic (periosteal reaction, sequestrum) and multinomial Logistic (lesion density).
  - **Study 1 event is “absence of the imaging feature,”** so OR>1 indicates higher odds of “no feature.”
- Pairwise lesion‑density comparisons use Bonferroni correction.
- Study 2 metrics: AUC, accuracy, sensitivity, specificity, precision, F1, and confusion matrix.

# Study 1: Imaging Features and Clinical Factors
## Research Questions
- How are imaging features distributed, and do they correlate with each other?
- Are imaging differences associated with clinical factors such as labs, disease origin, medication, or timing?

## Clinical Profile (Report Tables 1–2)
- Primary disease: breast cancer 57, lung cancer 42, prostate cancer 26, multiple myeloma 22, osteoporosis 15, renal cancer 12, rheumatoid arthritis 4, other 8.
- Stage distribution: stage 2 (11.8%), stage 3 (88.2%).
- Normal lab proportions: Hb 59.7%, albumin 39.8%, calcium 68.3%, glucose 75.3%.
- Medication types (report grouping): BPs 64.9%, DMB 4.9%, BPs+DMB 9.7%, anti‑angiogenic/immune 4.3%, anti‑resorptive + anti‑angiogenic 16.2%.
- Symptom‑to‑admission time: median 6 [4,12] months.
- **Note**: the single “other/unknown” case (n=1) is removed from the medication pie chart for clarity.

## Imaging Distribution and Inter‑Feature Association (Report 3.2)
- Periosteal reaction 82 cases (44.1%); sequestrum separation 51 cases (27.4%).
- Lesion density: destructive 66.1%, sclerotic 25.3%, mixed 8.6%.
- Inter‑feature association:
  - Periosteal vs sequestrum: χ²=6.14, P=0.01.
  - Sequestrum vs density: χ²=25.2, P<0.01.
  - Periosteal vs density: χ²=4.23, P=0.12 (not significant).

**Figure 1 Imaging distribution**
![Imaging distribution](/images/projects/mronj-study1/imaging_distribution.svg)
- Destructive pattern dominates (66.1%), consistent with late‑stage structural damage.
- Sequestrum is present in only 27.4%, supporting a longer timeline for formation.
- Periosteal reaction appears in 44.1%, suggesting inflammation is not universal.

**Figure 2 Primary disease distribution (report grouping)**
![Primary disease (report grouping)](/images/projects/mronj-study1/primary_disease_report.svg)
- Malignancy with bone metastasis plus multiple myeloma dominates the cohort.
- Breast/lung/prostate cancer contribute most, reflecting the major treatment populations.
- Benign disease is less frequent but still clinically meaningful for MRONJ risk.

**Figure 3 Medication type distribution (report grouping)**
![Medication types (report grouping)](/images/projects/mronj-study1/drug_type_report.svg)
- BPs are the main exposure source, consistent with established MRONJ mechanisms.
- Combined or anti‑angiogenic regimens are non‑trivial, indicating complex systemic therapy.
- A single “other/unknown” case is excluded to avoid a misleading slice.

**Figure 4–6 Imaging associations**
![Periosteal vs sequestrum](/images/projects/mronj-study1/periosteal_vs_sequestrum.svg)
![Sequestrum vs lesion density](/images/projects/mronj-study1/sequestrum_vs_lesion.svg)
![Periosteal vs lesion density](/images/projects/mronj-study1/periosteal_vs_lesion.svg)
- Sequestrum is concentrated within destructive lesions (94.1%), aligning with necrosis progression.
- Absence of periosteal reaction shows higher sequestrum proportion (34.6% vs 18.3%), suggesting different pathways.
- Density patterns do not shift strongly by periosteal reaction, implying limited structural coupling.

## Imaging–Clinical Associations (Report 3.3)
### 1) Periosteal reaction
- **Univariate**: Hb status (χ²=5.708, P=0.02), primary disease grouping (χ²=11.108, P=0.004), age (OR=1.033, P=0.04).
- **Multivariable**: Hb abnormality increases periosteal reaction (Hb normal → higher odds of “no periosteal reaction,” OR=2.13, P=0.017). Benign primary disease strongly favors no periosteal reaction (OR=8.22, P=0.007).
  - Hb likely captures systemic condition and inflammatory burden that influences periosteal response.
  - Benign disease shows less periosteal reaction, consistent with a different systemic milieu.
  - Age effect is modest once labs and disease type are accounted for.

### 2) Sequestrum separation
- **Univariate**: calcium status (χ²=6.426, P=0.01), symptom‑to‑admission time (P<0.001).
- **Multivariable**: symptom duration remains independent (OR=0.947, P=0.001).
  - Longer symptom duration predicts higher sequestrum formation.
  - Calcium appears in univariate only, suggesting confounding by timing and overall status.
  - Early intervention may interrupt the necrotic separation pathway.

### 3) Lesion density (destructive/sclerotic/mixed)
- **Univariate**: symptom duration (H=10.557, P<0.01).
- **Bonferroni**: sclerotic vs destructive differs (P=0.003); other pairs not significant.
- **Multivariable**: overall model significant (LR χ²=16.182, P=0.013); only symptom duration contributes independently.
  - Longer duration shifts lesions toward destructive density.
  - Mixed pattern is heterogeneous, with no stable independent predictors.
  - Medication and primary disease show limited direct effect on density type.

**Figure 7 Symptom‑to‑admission time vs lesion pattern (violin)**
![Symptom time by lesion](/images/projects/mronj-study1/symptom_time_by_lesion.svg)
- Destructive lesions show longer median duration (~9 months) and wider spread.
- Sclerotic lesions cluster at shorter durations (median ~6 months).
- Mixed lesions span both ranges, consistent with a transitional phenotype.

**Figure 8–11 Multivariable models (Study 1)**
![Periosteal model](/images/projects/mronj-study1/forest_periosteal.svg)
![Sequestrum model](/images/projects/mronj-study1/forest_sequestrum.svg)
![Lesion pattern (sclerotic vs destructive)](/images/projects/mronj-study1/forest_lesion_2.svg)
![Lesion pattern (mixed vs destructive)](/images/projects/mronj-study1/forest_lesion_3.svg)
- OR>1 indicates higher odds of “no feature,” per Study 1 event definition.
- Hb status and primary disease dominate the periosteal model.
- Symptom duration drives sequestrum and density models most consistently.
- Wide intervals in the mixed‑pattern model reflect limited sample size.

# Study 2: Imaging Features and Surgical Outcomes
## Research Questions
1) Do imaging features relate to surgical outcomes?
2) Can a combined imaging + clinical model predict prognosis?

## Outcome Definition and Follow‑up
- Follow‑up at 1 week, 1 month, 3 months, and 6 months post‑op.
- **Healed**: wound closure by 1 month with no infection.
- **Non‑healed**: persistent infection/non‑closure at 1 month despite debridement.
- **Recurrence**: MRONJ re‑appearing at any time after healing.

## Univariate Findings (Report 3.1)
- Sequestrum separation is significant (χ²=4.019, P=0.045); presence relates to better outcomes.
- Lesion density is significant (χ²=7.559, P=0.023); destructive heals best (73.2%), sclerotic worst (51.1%).
- Periosteal reaction is not significant (P=0.973).

**Figure 12 Outcome distribution**
![Outcome distribution](/images/projects/mronj-study2/outcome_distribution.svg)
- Overall healing rate is 67.2%, indicating surgical effectiveness.
- 32.8% non‑healed/recurrence highlights a sizable risk subgroup.
- Outcome spread supports the need for pre‑operative risk stratification.

**Figure 13–15 Imaging vs outcome**
![Periosteal vs outcome](/images/projects/mronj-study2/outcome_by_periosteal.svg)
![Sequestrum vs outcome](/images/projects/mronj-study2/outcome_by_sequestrum.svg)
![Lesion density vs outcome](/images/projects/mronj-study2/outcome_by_lesion.svg)
- Sequestrum‑positive cases heal more often (78.4% vs 63.0%), suggesting clearer necrotic boundaries.
- Sclerotic lesions have the lowest healing rate (51.1%), possibly reflecting poor vascularity.
- Periosteal reaction shows nearly identical healing rates, reinforcing its limited prognostic value.

## Prognostic Model and Performance
- **Performance**: AUC=0.770, ACC=0.672, sensitivity=0.598, specificity=0.817.
- **Drivers**: surgical strategy shows stronger, more stable effects than imaging variables alone.

**Figure 16 ROC curve**
![ROC curve](/images/projects/mronj-study2/roc_curve.svg)
- AUC 0.770 indicates moderate discrimination.
- The curve is clearly above the random baseline, confirming predictive signal.
- External validation is still required before clinical deployment.

**Figure 17 Confusion matrix**
![Confusion matrix](/images/projects/mronj-study2/confusion_matrix.svg)
- On the model subset, false negatives for non‑healed/recurrence remain substantial.
- Healing prediction is more reliable than non‑healing prediction.
- Adding quantitative imaging features may improve sensitivity for high‑risk cases.

**Figure 18 Multivariable Logistic model**
![Multivariable model (all variables)](/images/projects/mronj-study2/forest_multivariate.svg)
- Surgical type coefficients are consistently positive and often significant.
- Imaging variables preserve directional effects but are weaker in magnitude.
- Lab indicators show limited impact, likely due to heterogeneity and sample size.

# Conclusions and Clinical Meaning
- Study 1: disease duration is the main driver of imaging structural change; sequestrum aligns with destructive patterns.
- Study 2: imaging features stratify outcomes, but surgical strategy is more directly predictive.
- Clinical implication: integrate imaging structure, symptom duration, and surgical plan for risk‑aware decision making.

## Alignment with Prior Knowledge
- **Consistent**: destructive lesions and sequestrum align with longer disease course.
- **Needs refinement**: periosteal reaction shows limited association with density or outcome, suggesting inflammatory rather than structural signaling.

## Data and Reproducibility
- All results are aggregated; no raw patient records are exposed.
- Full‑variable coefficient tables are embedded below.

### Study 1: Full Coefficient Tables
#### Periosteal reaction model (all variables)

| Variable                          |   Coef | OR (95% CI)          |     P |
|:----------------------------------|-------:|:---------------------|------:|
| Intercept                         | -1.925 | 0.146 (0.018-1.210)  | 0.074 |
| Age                               |  0.024 | 1.024 (0.991-1.058)  | 0.151 |
| Hemoglobin normal                 |  0.757 | 2.131 (1.144-3.971)  | 0.017 |
| Primary disease: multiple myeloma |  0.264 | 1.302 (0.515-3.287)  | 0.577 |
| Primary disease: benign           |  2.106 | 8.215 (1.788-37.736) | 0.007 |

#### Sequestrum separation model (all variables)

| Variable                  |   Coef | OR (95% CI)           | P      |
|:--------------------------|-------:|:----------------------|:-------|
| Intercept                 |  2.708 | 14.993 (5.519-40.729) | <0.001 |
| Symptom-to-admission time | -0.055 | 0.947 (0.916-0.978)   | 0.001  |
| Albumin normal            | -0.011 | 0.989 (0.427-2.293)   | 0.980  |
| Hemoglobin normal         | -0.752 | 0.471 (0.201-1.105)   | 0.084  |
| Calcium normal            | -0.838 | 0.432 (0.175-1.070)   | 0.070  |

#### Lesion pattern model (sclerotic vs destructive)

| Variable                   |   Coef | OR (95% CI)         |     P |
|:---------------------------|-------:|:--------------------|------:|
| Intercept                  |  0.543 | 1.720 (0.512-5.787) | 0.381 |
| Symptom-to-admission time  | -0.078 | 0.925 (0.874-0.980) | 0.008 |
| BPs + DMB combination      |  0.878 | 2.406 (0.841-6.884) | 0.102 |
| Primary disease: malignant | -1.035 | 0.355 (0.117-1.074) | 0.067 |

#### Lesion pattern model (mixed vs destructive)

| Variable                   |   Coef | OR (95% CI)         |     P |
|:---------------------------|-------:|:--------------------|------:|
| Intercept                  | -1.054 | 0.348 (0.082-1.484) | 0.154 |
| Symptom-to-admission time  | -0.012 | 0.988 (0.937-1.042) | 0.66  |
| BPs + DMB combination      | -0.114 | 0.893 (0.102-7.839) | 0.918 |
| Primary disease: malignant | -0.965 | 0.381 (0.092-1.583) | 0.184 |

### Study 2: Prognostic Model Coefficients
#### Study 2 full multivariable Logistic coefficients

| Variable                                          |   Coef | OR (95% CI)            |     P |
|:--------------------------------------------------|-------:|:-----------------------|------:|
| Intercept                                         | -0.293 | 0.746 (0.043-12.826)   | 0.84  |
| Age                                               |  0.004 | 1.004 (0.964-1.045)    | 0.861 |
| Symptom-to-admission time                         | -0.001 | 0.999 (0.960-1.039)    | 0.949 |
| Medication duration (months)                      | -0.006 | 0.995 (0.981-1.008)    | 0.414 |
| Sex (male)                                        |  0.094 | 1.099 (0.505-2.393)    | 0.812 |
| Pre-op dental treatment                           | -0.738 | 0.478 (0.214-1.069)    | 0.072 |
| Periosteal reaction                               | -0.457 | 0.633 (0.272-1.472)    | 0.288 |
| Sequestrum separation                             |  0.376 | 1.456 (0.536-3.955)    | 0.461 |
| Hemoglobin normal                                 |  0.68  | 1.974 (0.805-4.839)    | 0.137 |
| Albumin normal                                    | -0.314 | 0.731 (0.264-2.025)    | 0.546 |
| Calcium normal                                    |  0.66  | 1.936 (0.804-4.662)    | 0.141 |
| Glucose normal                                    |  0.006 | 1.007 (0.431-2.350)    | 0.988 |
| Lesion pattern: sclerotic                         | -0.474 | 0.623 (0.250-1.550)    | 0.309 |
| Lesion pattern: mixed                             | -0.199 | 0.820 (0.202-3.320)    | 0.781 |
| Primary disease: multiple myeloma                 |  0.672 | 1.958 (0.491-7.815)    | 0.341 |
| Primary disease: benign                           |  0.858 | 2.359 (0.608-9.160)    | 0.215 |
| Medication: DMB                                   | -0.559 | 0.572 (0.120-2.723)    | 0.483 |
| Medication: BPs + DMB                             | -0.109 | 0.896 (0.254-3.169)    | 0.865 |
| Medication: immune/anti-angiogenic                |  0.452 | 1.572 (0.188-13.142)   | 0.677 |
| Medication: BPs + immune/anti-angiogenic          | -0.868 | 0.420 (0.130-1.358)    | 0.147 |
| Medication: DMB + immune/anti-angiogenic          | -0.202 | 0.817 (0.063-10.626)   | 0.877 |
| Surgery: block resection + reconstruction         |  1.433 | 4.192 (0.856-20.539)   | 0.077 |
| Surgery: segmental resection (no reconstruction)  |  1.815 | 6.144 (1.211-31.166)   | 0.028 |
| Surgery: submandibular gland transfer + plate     |  1.454 | 4.278 (1.601-11.433)   | 0.004 |
| Surgery: chin flap + plate                        |  2.024 | 7.570 (1.793-31.967)   | 0.006 |
| Surgery: free vascularized osteomyocutaneous flap |  2.824 | 16.851 (1.734-163.761) | 0.015 |
