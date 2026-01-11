---
layout: single
title: "MRONJ Surgical Outcome Analysis (Detailed)"
permalink: /projects/mronj-surgical-outcome-analysis/
author_profile: true
---

## Overview
MRONJ surgical outcomes vary widely, and clinicians often rely on imaging cues when deciding timing and scope of intervention. The central question of this project is simple but clinically important: **which imaging features are meaningfully associated with postoperative prognosis**, and can those associations help us prioritize patients and refine surgical planning? We focus on three routinely reported imaging features and ask whether they carry prognostic information beyond chance.

To answer this, we use a hypothesis‑testing framework built on univariate and multivariate logistic regression. Each feature is evaluated on its own and then jointly, so we can distinguish signals that appear in isolation from those that remain after accounting for other imaging information. The results below are aggregated and de‑identified, and are presented to support careful interpretation rather than definitive prediction.

**Report download:** [Aggregated analysis report](/files/mronj-analysis-report.txt)

**Chinese version:** [中文页面](/projects/mronj-surgical-outcome-analysis-zh/)

## Data profiling (visual)
![Outcome distribution](/images/projects/mronj/outcome_distribution.png)

![Missingness by variable](/images/projects/mronj/missing_rates.png)

![Imaging feature distributions](/images/projects/mronj/imaging_distribution.png)

These figures summarize the outcome balance, missingness across key variables, and the distribution of imaging features. They help explain where statistical power may be limited and where imbalance can bias model behavior.

## Study question and hypotheses
The statistical question is framed as a sequence of hypothesis tests. For each predictor \\(X_j\\), we test \\(H_0: \\beta_j = 0\\) (Wald test). For multi‑level categorical features, we use a likelihood‑ratio test (LLR) to assess overall significance. This approach lets us quantify which imaging signals are supported by the data and which are weak or uncertain.

## Outcome and predictors
- Outcome: \\(Y=1\\) for **1A有效**, \\(Y=0\\) for **2B/C/D/E**.
- Imaging predictors:
  - 骨膜反应（1是2否）
  - 死骨分离（1是2否）
  - 病变特点（1破坏2硬化3混合）

## Statistical model
We fit a binary logistic regression:

\\[
\\log\\frac{P(Y=1\\mid X)}{1-P(Y=1\\mid X)} = \\beta_0 + \\sum_j \\beta_j X_j
\\]

Each \\(X_j\\) is tested with Wald tests, and the imaging multivariable model is evaluated by an LLR test.

## Results snapshot (aggregate)
The tables below summarize model performance and the strength of association for each imaging feature.

**Model metrics**

| Metric | Value |
| --- | --- |
| AUC | 0.730 |
| Accuracy | 0.731 |
| Sensitivity | 0.928 |
| Specificity | 0.328 |
| Precision | 0.739 |
| F1 | 0.823 |
| Threshold (accuracy-optimized) | 0.344 |
| LLR p-value (imaging multivariable) | 0.0678 |
| Pseudo R\\(^2\\) | 0.037 |

**Imaging univariate tests**

| Feature | Test | P-value | Direction |
| --- | --- | --- | --- |
| 骨膜反应（1是2否） | Wald | 0.9730 | 负向 |
| 死骨分离（1是2否） | Wald | 0.0479 | 正向 |
| 病变特点（1破坏2硬化3混合） | LLR | 0.0260 | Overall |

## Key findings
Across single‑feature models, **死骨分离** and **病变特点** show evidence of association (P < 0.05). However, when the three imaging features are evaluated jointly, the overall evidence becomes borderline (LLR p-value 0.0678). This suggests that part of the signal may be shared across features rather than independent. For prediction, a class‑weighted logistic model with regularization improves accuracy to 0.731, but does so by favoring sensitivity over specificity at the chosen threshold.

## Visualizations and interpretation (aggregate)
**Model performance overview**

![Model metrics](/images/projects/mronj/metrics_bar.png)

Interpretation: AUC around 0.73 indicates improved discrimination under the predictive model. Accuracy rises to 0.731, driven by high sensitivity, while specificity remains low, reflecting a threshold that prioritizes detecting positives.

**Confusion matrix**

![Confusion matrix](/images/projects/mronj/confusion_matrix.png)

Interpretation: The confusion matrix shows many true positives but still a notable number of false positives. This reflects class imbalance and the accuracy‑optimized threshold, which favors sensitivity to avoid missing positive cases.

**Imaging feature significance**

![Imaging p-values](/images/projects/mronj/imaging_pvalues.png)

Interpretation: Univariate signals are strongest for **死骨分离** and **病变特点**, while **骨膜反应** shows little evidence of association. This suggests that not all imaging cues contribute equally to prognosis.

**Odds ratios with 95% CI**

![Odds ratios](/images/projects/mronj/odds_ratio.png)

Interpretation: Several confidence intervals cross 1.0, indicating uncertainty. This is consistent with the borderline multivariable LLR p-value and suggests limited independent effects under joint testing.

**ROC curve**

![ROC curve](/images/projects/mronj/roc_curve.png)

Interpretation: The ROC curve indicates discrimination above chance and stronger than the earlier model. This suggests that adding clinical and intervention variables plus regularization improves predictive separation.

## Discussion (hypothesis-testing view)
These results are consistent with a setting where imaging features are correlated: a strong univariate signal can weaken after joint testing because the model is separating overlapping information. Sparse categories and complete‑case filtering reduce effective sample size and widen uncertainty. For prediction, we mitigate imbalance using class weights and L2 regularization, which improves overall accuracy but still leaves a sensitivity‑specificity trade‑off that depends on the chosen threshold.

## Clinical interpretation and insight
From a clinical standpoint, the signal for **死骨分离** and **病变特点** aligns with intuition: clearer sequestrum separation and lesion pattern often reflect the maturity and biological behavior of the disease. The weak signal for **骨膜反应** may indicate limited incremental information or measurement variability in routine imaging. Overall, the current evidence supports using imaging features for **screening or risk stratification**, while recognizing that definitive prognostic use requires stronger, more stable signals and better control of uncertainty.

## Practical insights
In practice, these results suggest a cautious but useful role for imaging: prioritize patients with high‑risk imaging profiles and interpret results in combination with clinical context. Methodologically, improving data completeness and reducing sparse categories will strengthen inference. Clinically, standardizing imaging annotations could reduce noise and help reveal more stable associations.

## Notes and next steps
- Improve data completeness to enable confounder-adjusted models.
- Merge sparse categories to reduce separation.
- Revisit threshold selection and validate with new data if available.
