# Fairness Definition Selection Tool

## 1. Introduction

This document presents the second component of the Fairness Audit Playbook: the **Fairness Definition Selection Tool**. This tool was developed in response to fairness concerns in a credit pre-approval system based on predicted income. After identifying historical patterns of discrimination and risks (via the Historical Context Assessment Tool), this tool helps teams select the fairness definition(s) best aligned with the system’s objectives, ethical constraints, and potential harms.

Fairness definitions are not neutral or interchangeable — they reflect specific assumptions about justice, rights, and acceptable trade-offs. This tool facilitates informed decision-making by translating theoretical definitions into implementable criteria and guiding teams through the selection process.

## 2. Fairness Definition Catalog

| Fairness Definition | Mathematical Formulation | Appropriate Use Cases | Limitations |
|----------------------|---------------------------|-------------------------|-------------|
| **Demographic Parity** | P(Ŷ=1|A=a) = P(Ŷ=1|A=b) | Useful in domains with historical exclusion or when equal representation is prioritized (e.g., public service eligibility, outreach systems). | May reduce accuracy when qualification base rates differ across groups. Can result in reverse discrimination. |
| **Equal Opportunity** | P(Ŷ=1 \| Y=1, A=a) = P(Ŷ=1 \| Y=1, A=b) | Prioritize when false negatives (e.g., denying qualified applicants) have higher harm. Requires reliable ground truth labels. | Does not address false positives. Depends on quality of labels, which may carry historical bias. |
| **Equalized Odds** | P(Ŷ=1 \| Y=y, A=a) = P(Ŷ=1 \| Y=y, A=b) for y in {0,1} | Use when both types of error (FP, FN) carry significant risk. Especially important in sensitive domains like criminal justice or healthcare. | Often requires complex implementation. Greater trade-offs with accuracy. |
| **Predictive Equality** | P(FP \| A=a) = P(FP \| A=b) | Prioritize when false positives cause the greatest harm (e.g., surveillance or penalization systems). | Doesn’t address fairness for truly qualified individuals. |
| **Sufficiency / Calibration** | P(Y=1 \| Ŷ=p, A=a) = P(Y=1 \| Ŷ=p, A=b) | Useful when exposing probabilistic scores (e.g., credit scoring). | Can be incompatible with other group fairness definitions. |

## 3. Decision Tree for Fairness Definition Selection

### Step 1: Historical Context Assessment
> **Q:** Has historical analysis revealed systemic exclusion or marginalization of protected groups (e.g., women, racial minorities)?

✅ Yes → Include **Demographic Parity** for monitoring purposes.

### Step 2: Error-Impact Analysis
> **Q:** Which error type has greater negative impact in this application?

✅ False Negatives → Select **Equal Opportunity** as primary definition.

- In the loan context, rejecting an applicant who is in fact eligible (i.e., under-predicting income) may worsen economic exclusion.

### Step 3: Exposure of Scores
> **Q:** Does the system expose probabilistic income scores or risk estimates to other systems or decision-makers?

✅ Yes → Add **Sufficiency/Calibration** as a supporting fairness goal.

## 4. Trade-Off Analysis

| Dimension | Description |
|----------|-------------|
| **Primary Fairness Definition** | Equal Opportunity (focus on minimizing disparities in true positive rate between groups). |
| **Historical Context Alignment** | Gender and socioeconomic exclusion are historically present in financial access. Using Equal Opportunity addresses legacy effects. |
| **Stakeholder Priorities** | Fair credit access and minimizing wrongful rejections are key priorities for both compliance and inclusion goals. |
| **Fairness Properties Not Guaranteed** | Demographic parity and predictive equality are not enforced as primary constraints. |
| **Implementation Implications** | May require threshold adjustments or post-processing to equalize TPR across groups. |
| **Monitoring Plan** | Monitor demographic parity and calibration gaps across intersectional groups. |

## 5. Usage Guide

### Implementation Process

1. **Review Historical Context Results**
   - Use the output of the Historical Context Assessment to identify marginalized groups.

2. **Apply Decision Tree**
   - Follow the questions in the selection flow to determine which definitions apply.

3. **Evaluate Legal and Stakeholder Considerations**
   - Consider regulatory compliance, ethical guidelines, and social expectations.

4. **Document Selection and Trade-Offs**
   - Use the trade-off template to record rationale and limitations.

5. **Share and Iterate**
   - Review with DEI teams, product owners, and legal if necessary. Adjust as the system evolves.

## 6. Case Study: Pre-Approval System Based on Income Prediction

### System Description
- Domain: Financial Services – Consumer Lending
- Task: Predict user's monthly income from self-reported and auxiliary data to pre-approve credit offers.
- Output: Income estimate and loan eligibility decision

### Fairness Challenges
- Income is a proxy for creditworthiness but is historically influenced by gender, race, and geography.
- False negatives (underestimating income of qualified users) risk reinforcing systemic exclusion.

### Selected Fairness Definitions
- ✅ **Primary:** Equal Opportunity
- ✅ **Monitoring:** Demographic Parity, Calibration

### Implications
- Income prediction thresholds may be adjusted to reduce group-based disparity in TPR.
- Calibration will be tracked to ensure that predicted income scores are equally accurate across subgroups.
- Demographic parity will be monitored but not enforced as a hard constraint to avoid reducing model performance.

---

This tool supports structured, justifiable fairness definition selection that balances ethical concerns, legal risk, and real-world feasibility.
