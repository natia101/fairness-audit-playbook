# 06_Case_Study.md

## Case Study: Fairness Audit for Income Prediction in Loan Pre-Approval System

---

## 1. System Context

**Use Case:** A banking institution developed a machine learning model to predict applicant income based on self-reported features, with the goal of pre-approving consumer loans. The model outputs a predicted income that serves as the basis for loan approval thresholds.

**Problem Type:** Regression (continuous prediction of income)

**Fairness Sensitivity:** Loan decisions are sensitive to both underprediction (rejection of qualified applicants) and overprediction (approving riskier applicants). Demographic disparities may lead to compounding financial exclusion.

---

## 2. Applying the Fairness Audit Playbook

### 2.1 Historical Context Assessment

- **Application Domain:** Financial lending.
- **Historical Patterns:**
  - Historical exclusion of women, youth, and low-income minorities from formal banking systems.
  - Systematic underestimation of women’s and informal workers’ income in loan evaluations.
  - Biases in data collection instruments used by credit bureaus.

- **Risk Classification:**
  | Historical Pattern | Severity | Likelihood | Relevance | Priority |
  |--------------------|----------|------------|-----------|----------|
  | Gender exclusion in credit markets | High (3) | High (3) | High (3) | 9 (Critical) |
  | Informal sector penalization | Medium (2) | High (3) | Medium (2) | 7 (High) |
  | Bias in income proxies | Medium (2) | Medium (2) | High (3) | 6 (High) |

---

### 2.2 Fairness Definition Selection

- **Primary Definition:** Equal Opportunity (focus on minimizing disparities in underprediction of qualified individuals)
- **Secondary Definition:** Demographic Parity (monitor approval rate balance)

**Rationale:**
- Underestimating income for protected groups leads to denial of credit.
- Stakeholders prioritize equitable access to loans.
- Regulatory frameworks emphasize non-discrimination in financial decisions.

---

### 2.3 Bias Source Identification

| Bias Type | Description | Evidence |
|----------|-------------|----------|
| Historical Bias | Legacy exclusion from credit databases | Gender and informal workers underrepresented |
| Measurement Bias | Income inferred through noisy or biased proxies (e.g., education level, zip code) | Correlation of proxies with gender and SES |
| Representation Bias | Dataset skewed toward formal-sector workers | Informal workers under-sampled |
| Learning Bias | Model underfits income ranges common to minorities | Higher residuals in specific groups |
| Evaluation Bias | No disaggregated evaluation in development phase | No fairness metrics reported initially |

- **Prioritization Example:**
  - Measurement Bias → High priority (Score = 4.3)
  - Representation Bias → Medium (Score = 3.6)

---

### 2.4 Fairness Metrics Selection and Calculation

**Metrics Chosen:**
- Absolute Residual Difference (by group)
- Positive/Negative Residual Difference (for harm sensitivity)
- Demographic Parity Difference (binary approval threshold)
- Intersectional Residual Difference

**Example Results:**

| Metric | Value | 95% CI | Interpretation |
|--------|-------|--------|----------------|
| Abs. Residual Diff (Gender) | 0.21 | [0.15, 0.28] | Women systematically underpredicted |
| Neg. Residual Diff (Low-income) | 0.24 | [0.17, 0.30] | Qualified applicants wrongly rejected |
| Demographic Parity Diff | 0.16 | [0.10, 0.22] | Lower approval for minority group |
| Intersectional (Young Women) | 0.29 | [0.20, 0.37] | Highest compound disparity |

---

### 2.5 Visualization Summary

- Fairness Disparity Chart: Bar plot of residual errors by gender, income bracket.
- Intersectional Heatmap: Gender × Age × Income group.
- Supplementary Table: Full metric breakdown + group sizes.

---

## 3. Insights and Recommendations

- **High Disparities Found**: Consistent underprediction in protected groups.
- **Primary Action**: Recalibrate model and retrain with better representation from informal sector.
- **Secondary Action**: Introduce fairness constraints during training; expand feature space to include more representative indicators.
- **Process Change**: Integrate fairness evaluation in standard MLOps pipeline with disaggregated dashboards.

---

## 4. Implementation Reflection

- **Challenges**:
  - Sparse data in high-risk groups.
  - Proxy variables encoding social bias.
  - Tension between precision and fairness.

- **Benefits of Playbook**:
  - Clear workflow from root causes to metrics.
  - Grounded technical evaluation.
  - Facilitates cross-functional communication (data, legal, product).

---

## 5. Future Monitoring

- Track group-wise approval rates and error trends quarterly.
- Trigger fairness reassessment on model updates.
- Monitor residual shifts across demographic slices.
- Institutionalize fairness reviews at compliance checkpoints.

---

> This case study demonstrates the value of integrating fairness into the entire ML lifecycle, providing actionable diagnostics and mitigation insights through the Fairness Audit Playbook.
