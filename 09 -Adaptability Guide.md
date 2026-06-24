# 09_Adaptability_Guide.md

## Adaptability Guide: Using the Fairness Audit Playbook Across Domains and Problem Types

This guide provides practical recommendations for adapting the Fairness Audit Playbook to various domains (e.g., healthcare, education, criminal justice) and technical problem types (e.g., classification, regression, ranking). The goal is to maintain methodological rigor while ensuring contextual relevance.

---

## 1. Domain Adaptation

### a. Key Considerations
- **Regulatory landscape:** What laws govern fairness and discrimination in the domain?
- **Historical harms:** Are there documented patterns of exclusion or inequity?
- **Stakeholders:** Who are the impacted users, and what values are prioritized?

### b. Examples of Contextual Questions

| Domain | Fairness Focus | Example |
|--------|----------------|---------|
| Healthcare | Equal access to diagnosis and treatment | Are false negatives (missed diagnoses) disproportionately affecting certain groups? |
| Education | Equitable learning opportunities | Are predictive models of student success amplifying achievement gaps? |
| Criminal Justice | Fair treatment under law | Are risk scores contributing to disparate sentencing outcomes? |

### c. Adaptation Tips
- Tailor the **historical context assessment** to the domain’s social and institutional history.
- Choose **fairness definitions** aligned with domain-specific risks (e.g., false negatives in healthcare).
- Engage **domain experts** when assessing bias sources and evaluating mitigation feasibility.

---

## 2. Technical Problem Type Adaptation

### a. Classification Problems
- Common in: Hiring, admissions, fraud detection
- Typical Metrics: True/false positive rate parity, demographic parity, equalized odds
- Special Considerations: Balance between accuracy and fairness across decision thresholds

### b. Regression Problems
- Common in: Credit scoring, pricing, income prediction
- Typical Metrics: Residual disparity, group loss bounds, bounded regret
- Special Considerations: Directional harm (e.g., underprediction vs. overprediction)

### c. Ranking Problems
- Common in: Resume screening, recommendation engines, content ranking
- Typical Metrics: Exposure parity, representation in top-k, NDCG difference
- Special Considerations: Fairness may depend on position in ranked list rather than binary outcomes

---

## 3. Adaptation Framework

| Component | What to Adapt | How |
|-----------|----------------|-----|
| 01_Historical_Context_Assessment | Focus areas | Align to systemic patterns relevant to new domain |
| 02_Fairness_Definition_Selection | Definitions + thresholds | Select based on dominant harm and stakeholder priorities |
| 03_Bias_Source_Identification | Pipeline stages | Modify taxonomy to include domain-specific data sources |
| 04_Fairness_Metrics_Tool | Metric set | Align to problem type and selected fairness definition |
| 07_Case_Study | Example system | Use real system from new domain for contextualization |

---

## 4. Organizational Considerations

- **Reuse Core Templates**: The tools are designed to be modular — adapt forms, not workflows.
- **Build Domain-Specific Libraries**: Maintain annotated examples, metrics, and risks per domain.
- **Encourage Localized Ownership**: Empower teams in each domain to own the fairness assessment process.

---

## 5. Final Note

> Fairness is not one-size-fits-all. But with the right scaffolding, the Playbook provides a structured foundation for adapting fairness assessments to any domain or problem type.
