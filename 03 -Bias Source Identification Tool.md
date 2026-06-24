# 03\_Bias\_Source\_Identification\_Tool

## 1. Overview

The **Bias Source Identification Tool** is the third component of the Fairness Audit Playbook. It is designed to help AI engineering teams systematically identify, analyze, and prioritize sources of bias throughout the machine learning lifecycle. It builds upon prior insights from the Historical Context Assessment and Fairness Definition Selection.

This tool is meant to be:

* Reusable across different projects.
* Adaptable to various domains (e.g., finance, health, HR).
* Aligned with fairness definitions selected in earlier stages.

---

## 2. Bias Type Taxonomy

Below is a structured taxonomy of bias types that commonly emerge in AI systems, each with key indicators and examples:

### 2.1 Historical Bias

* **Definition**: Bias stemming from pre-existing societal inequalities that are reflected in data.
* **Indicators**: Target variables reflect discrimination; correlations reproduce societal hierarchies.
* **Example**: Income prediction models reflecting labor market gender/racial gaps.

### 2.2 Representation Bias

* **Definition**: Bias due to underrepresentation or skewed sampling in data collection.
* **Indicators**: Data coverage does not reflect target population; quality gaps across groups.
* **Example**: A loan system trained on salaried urban populations but applied to informal rural earners.

### 2.3 Measurement Bias

* **Definition**: Bias introduced by the way variables are operationalized or proxied.
* **Indicators**: Proxy variables with different accuracy across groups; inconsistent label generation.
* **Example**: Using declared occupation as a proxy for income.

### 2.4 Aggregation Bias

* **Definition**: Bias from applying a single model to populations with distinct data relationships.
* **Indicators**: Homogeneous models on heterogeneous populations; unbalanced errors.
* **Example**: A scoring model ignoring economic structure differences between rural and urban areas.

### 2.5 Learning Bias

* **Definition**: Bias from algorithm design, optimization, or overfitting to dominant patterns.
* **Indicators**: Disparities in error rates; penalization of minority patterns.
* **Example**: Income predictions overfit to higher-income groups, inflating error for low-income applicants.

### 2.6 Evaluation Bias

* **Definition**: Bias from evaluation data or metrics that fail to represent real-world use.
* **Indicators**: Unrepresentative test data; lack of disaggregation.
* **Example**: Model validated on salaried workers but deployed on gig economy workers.

### 2.7 Deployment Bias

* **Definition**: Bias arising from how a system is used in practice.
* **Indicators**: Context shift; feedback loops.
* **Example**: A pre-approval system reinforcing patterns of exclusion over time through retraining.

---

## 3. Detection Methodology

Each bias type can be investigated through targeted techniques. These combine the outcomes of the previous tools with specific quantitative/qualitative checks.

### Detection Workflow

1. **Consult Historical Context Assessment** → Identify historical risks.
2. **Consult Fairness Definition Selection** → Focus on most relevant fairness criteria.
3. **Apply targeted detection for each bias type:**

| Bias Type           | Key Technique                                   | Example Application                                              |
| ------------------- | ----------------------------------------------- | ---------------------------------------------------------------- |
| Historical Bias     | Compare output distributions by protected group | Check if predicted income aligns with known disparities          |
| Representation Bias | Demographic benchmark comparison                | % rural vs urban applicants in training vs national census       |
| Measurement Bias    | Analyze proxy accuracy across groups            | Check if income proxy (job title) performs differently by gender |
| Aggregation Bias    | Segment-specific performance                    | Compare model error by economic region                           |
| Learning Bias       | Evaluate fairness metrics by group              | False negative rates by gender or age                            |
| Evaluation Bias     | Review test set vs deployment                   | Audit if test data covers gig workers                            |
| Deployment Bias     | Feedback loop simulation                        | Evaluate impact of retraining on marginal groups                 |

---

## 4. Prioritization Framework

Each identified bias source is scored using the following five dimensions:

| Dimension                | Description                              | Scale |
| ------------------------ | ---------------------------------------- | ----- |
| Severity                 | Harm if unaddressed                      | 1–5   |
| Scope                    | % of decisions affected                  | 1–5   |
| Persistence              | Risk of compounding via feedback loops   | 1–5   |
| Historical Alignment     | Match with known discriminatory patterns | 1–5   |
| Intervention Feasibility | Ease of mitigation                       | 1–5   |

**Priority Score** = (Severity × 0.3) + (Scope × 0.2) + (Persistence × 0.2) + (Historical Alignment × 0.2) + (Intervention Feasibility × 0.1)

| Priority Category | Score     |
| ----------------- | --------- |
| High              | ≥ 4.0     |
| Medium            | 3.0 – 3.9 |
| Low               | < 3.0     |

---

## 5. Case Study: Income Predictor in Loan Pre-Approval System

### Context

A bank develops a model that predicts a user's income based on limited self-reported variables (e.g., occupation, education level, homeownership, etc.) to pre-approve personal loans.

### Identified Bias Sources

| Bias Source                                  | Type                | Evidence                                                       | Priority Score |
| -------------------------------------------- | ------------------- | -------------------------------------------------------------- | -------------- |
| Overrepresentation of salaried urban workers | Representation Bias | Informal workers underrepresented in training data             | 4.2 (High)     |
| Use of declared occupation as proxy          | Measurement Bias    | Proxy performs worse for women and gig workers                 | 3.9 (Medium)   |
| Ignoring regional income disparities         | Aggregation Bias    | Same model applied nationwide despite cost of living variation | 4.0 (High)     |
| Higher false negatives for young applicants  | Learning Bias       | FN rate 20% higher for 18–24 vs baseline                       | 4.1 (High)     |
| Evaluation on bank clients only              | Evaluation Bias     | Excludes unbanked population now being targeted                | 3.7 (Medium)   |

### Implications

* **Representation** and **learning biases** are highest risk.
* Measurement and evaluation also relevant for monitoring.
* Regional customization may help address aggregation bias.

---

## 6. Implementation Guidelines

* **Recommended Timing**: Mid-development phase, before model deployment.
* **Team Composition**: Include data scientists, domain experts, and ethics stakeholders.
* **Inputs Required**: Access to training/test data, fairness definitions, and historical patterns.
* **Outputs**: Prioritized list of bias sources with mitigation strategies.

---

## 7. Future Improvements

* Automate scoring via dashboard.
* Link risk scores to mitigation workflows.
* Develop standardized detection scripts for each bias type.
* Incorporate user feedback loops into deployment bias detection.

---

## 8. References

* Fairness and Machine Learning, Barocas, Hardt & Narayanan (2024)
* Turing College Platform Materials, Unit 5 – Bias Sources
* Internal case studies shared under NDA (not published)

---
