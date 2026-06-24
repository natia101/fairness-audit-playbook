# 04_Fairness_Metrics_Tool.md

## 1. Overview

The **Fairness Metrics Tool** is the fourth component of the Fairness Audit Playbook. It provides AI teams with a structured framework to select, implement, validate, and interpret fairness metrics in alignment with the historical patterns, fairness definitions, and bias sources identified in earlier phases.

This tool helps ensure that fairness assessments are grounded in rigorous quantitative evaluation rather than intuition or aesthetics. It is intended to be applicable across domains and ML problem types.

---

## 2. Metric Selection Methodology

### 2.1 Overview

Selecting fairness metrics involves mapping fairness definitions to appropriate quantitative measures. This must account for the problem type (classification, regression, ranking), error trade-offs, probabilistic outputs, and stakeholder priorities.

### 2.2 Step-by-Step Metric Selection

#### Step 1: Identify Problem Type
- **Classification**: Outcome is discrete (e.g., approve/reject loan).
- **Regression**: Outcome is continuous (e.g., predict income level).
- **Ranking**: Output is a ranked list (e.g., loan offer priority).

#### Step 2: Select Fairness Definition
Refer to your selected fairness definitions from the prior tool (e.g., Demographic Parity, Equal Opportunity, Equalized Odds, Predictive Equality, Individual Fairness).

#### Step 3: Match to Metrics

##### Classification Problems:
- **Demographic Parity** → _Demographic Parity Difference_: P(Ŷ=1|A=a) - P(Ŷ=1|A=b)
- **Equal Opportunity** → _True Positive Rate (TPR) Difference_: P(Ŷ=1|Y=1,A=a) - P(Ŷ=1|Y=1,A=b)
- **Equalized Odds** → _TPR and FPR Differences_: Evaluate disparities in both types of errors.

##### Regression Problems:
- **Statistical Parity** → _Group Outcome Mean Difference_
- **Bounded Group Loss** → _Max Group Loss_, _Group Error Ratio_
- **Individual Fairness** → _Input-Output Sensitivity_, _Consistency Metrics_

##### Ranking Problems:
- **Exposure Parity** → _Exposure Ratio_, _NDCG Difference_
- **Representation Parity** → _Top-k Proportion Difference_, _Group Representation Ratio_

#### Step 4: Determine Error Direction Sensitivity (for Regression)
- Overprediction more harmful? → Include _Positive Residual Difference_
- Underprediction more harmful? → Include _Negative Residual Difference_
- Both harmful? → Use _Absolute Residual Difference_

#### Step 5: Calibrated Outputs (Optional)
- If the model outputs probabilistic scores used in decision-making:
  - Use _Calibration by Group_, _Brier Score Decomposition_, or _Prediction Interval Coverage_.

---

## 3. Statistical Validation

### 3.1 Confidence Intervals via Bootstrapping
- Resample the dataset with replacement multiple times (e.g., 1000 iterations).
- Compute fairness metrics on each sample.
- Derive 95% confidence intervals.

### 3.2 Bayesian Methods for Small Sample Sizes
- For groups with <100 instances, bootstrapping is unstable.
- Use Bayesian estimations with weakly informative priors.
- Report credible intervals and include sample size warnings.

### 3.3 Significance Testing (Optional)
- Conduct permutation tests to determine if observed disparities are statistically significant.
- Report p-values or effect sizes, with a threshold such as p < 0.05.

---

## 4. Visualization and Reporting Templates

### 4.1 Fairness Disparity Chart
- Bar chart with metrics (e.g., TPR) per group.
- Include error bars representing 95% confidence intervals.
- Use color to highlight statistically significant disparities.
- Reference line for acceptable threshold (e.g., ≤0.1 difference).

### 4.2 Intersectional Fairness Heatmap
- Rows = Protected group intersections (e.g., Gender × Age)
- Columns = Fairness metrics
- Color gradient indicates disparity magnitude.
- Opacity or cell size reflects sample size.

### 4.3 Supplementary Tables
- Present raw metric values, confidence intervals, and sample sizes.
- Highlight metrics above threshold.

---

## 5. Case Study: Income Predictor in Loan Pre-Approval System

### 5.1 Context
A banking institution deploys an AI model that predicts a user’s income from self-reported data to determine pre-approval for loans. Historical context and fairness definition analysis led to the selection of Equal Opportunity and Demographic Parity as primary fairness definitions.

### 5.2 Selected Metrics
- **True Positive Rate Difference (TPR Diff)**: Based on Equal Opportunity
- **False Negative Rate Difference (FNR Diff)**: For more granularity
- **Demographic Parity Difference**: For secondary monitoring
- **Intersectional TPR Difference**: For compounded group analysis

### 5.3 Implementation Results

| Metric | Value | 95% CI | Interpretation |
|--------|-------|--------|----------------|
| TPR Diff (Gender) | 0.17 | [0.12, 0.22] | Significant disparity disadvantaging women |
| FNR Diff (Age) | 0.21 | [0.15, 0.27] | Higher FN for young adults |
| Demographic Parity Diff | 0.13 | [0.09, 0.18] | Approval rates not equal across groups |
| Intersectional TPR (Young Women) | 0.25 | [0.18, 0.32] | Compounded disadvantage observed |

_All disparities were statistically significant (p < 0.01)._

### 5.4 Visualization Summary
- Fairness Disparity Bar Chart for gender and age
- Intersectional Heatmap: Gender × Age × Region
- Raw metric tables included in appendix

---

## 6. Implementation Guidelines

| Element | Recommendation |
|---------|----------------|
| **When to use** | After model training, before deployment |
| **Who is involved** | Data scientists, fairness analysts, product stakeholders |
| **Inputs required** | Model predictions, true labels, protected attributes |
| **Tools suggested** | Python (Fairlearn, AIF360), R, dashboard integration |
| **Time estimate** | 2–4 hours per fairness definition |
| **Dependencies** | Completion of prior tools (definitions + bias sources) |

### Best Practices
- Always disaggregate metrics.
- Compare both group-level and intersectional disparities.
- Use statistical intervals, not only point estimates.
- Document trade-offs if metrics conflict.

---

## 7. Future Improvements
- Automate reporting via dashboard tools.
- Incorporate longitudinal fairness tracking.
- Expand to causal fairness metrics where appropriate.
- Integrate stakeholder-defined acceptable thresholds.
- Add model-specific calibration and uncertainty tools.

---

## 8. References
- Turing College Platform Materials, Unit 5 – Fairness Metrics
- *Fairness and Machine Learning* (Barocas, Hardt & Narayanan, 2024)
- Mitchell et al. (2019) – Model Cards for Model Reporting
- AIF360, Fairlearn Documentation

---

This tool supports the technical foundation for evaluating fairness in practice and ensures that fairness goals are not only well-defined but also measurable and trackable over time.
