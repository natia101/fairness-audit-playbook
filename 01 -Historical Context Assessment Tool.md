# 01 – Historical Context Assessment Tool

## 1. Tool Overview

This tool helps technical teams assess how historical inequalities may influence the design and outcomes of AI systems. By foregrounding social and institutional context, it enables fairness assessments to address the root causes of bias — not just its symptoms.

This version is applied to a real use case: a predictive model that estimates a person’s income to determine whether they qualify for a pre-approved personal loan. While efficient, this approach risks reproducing long-standing patterns of exclusion from financial systems.

The tool includes:
- A structured questionnaire
- A historical risk classification matrix
- Implementation steps for integrating results into fairness audits

---

## 2. Historical Context Assessment Questionnaire

### Section A: Domain and Application Context

**What domain does the system operate in?**  
Consumer finance. The system is used by a bank to determine whether users qualify for a pre-approved loan, based on predicted income.

**What documented patterns of discrimination exist in this domain?**  
- Redlining and discriminatory lending practices that excluded racial minorities and poor neighborhoods from financial services.
- Legal and informal barriers to women’s financial independence until the late 20th century.
- Ongoing exclusion of informal workers, especially migrants, domestic workers, and day laborers, from access to formal credit.

**Which groups were historically disadvantaged?**  
- Racialized groups (e.g., Afro-descendants, Indigenous communities)  
- Women and single mothers  
- Informal and undocumented workers  
- Migrant communities  
- People with unstable or non-traditional employment

---

### Section B: Data and Representation Analysis

**What historical data sources are used or reflected in the system?**  
Self-declared attributes such as education, occupation, and region — which may be compared against legacy data like employment registries or income benchmarks derived from formal labor markets.

**How were these datasets shaped historically?**  
- Formal education levels reflect past (and ongoing) inequalities in access to schooling.
- Occupation categories reproduce class and gender hierarchies (e.g., caregiving vs. technical fields).
- Regional classifications may reflect patterns of segregation and investment disparities.

**How have categories like creditworthiness, risk, or employment been defined over time?**  
These concepts have historically favored formal, white-collar, male-coded work, and penalized informal, feminized, or community-based labor. Creditworthiness itself has often served as a gatekeeping tool shaped by access to documentation, networks, and formal market participation.

**Do measurement strategies embed bias?**  
Yes. Using features like “occupation” or “education level” as direct income proxies assumes uniform returns across social groups — which contradicts the realities of discrimination in the labor market.

---

### Section C: Technology Transition Patterns

**What previous systems were used for this purpose?**  
Credit officers relying on manual review and documentation. Automated scoring systems based on traditional credit reports and formal income.

**How did those systems encode inequality?**  
- Relied on documentation only available to formally employed or asset-owning individuals.  
- Penalized users without regular payslips, credit history, or formal bank accounts.  
- Reinforced exclusion of migrants and precarious workers.

**What additional risks does automation introduce?**  
- Speed and scale of exclusion without human review.  
- Increased opacity in how features are weighted.  
- Potential for feedback loops where excluded populations remain invisible to the system.

---

## 3. Historical Context Risk Classification Matrix

| Historical Pattern                             | System Components Affected              | Severity | Likelihood | Relevance | Priority Score | Notes |
|------------------------------------------------|-----------------------------------------|----------|------------|-----------|----------------|-------|
| Redlining via geography and occupation         | Feature selection (region, job title)   | High (3) | High (3)   | High (3)  | 9 – Critical    | Patterns of exclusion replicated via proxies |
| Informal labor exclusion                       | Model inputs; documentation criteria    | High (3) | High (3)   | Medium (2)| 8 – Critical    | Informality penalized across contexts |
| Gender bias in occupational value              | Feature weighting; target label         | Medium (2)| Medium (2) | Medium (2)| 6 – High        | Feminized jobs undervalued; wage gap persists |
| Education as class and race proxy              | Feature set (education level)           | Medium (2)| Medium (2) | High (3)  | 6 – High        | Unequal access to quality education by region |
| Formality as a proxy for trustworthiness       | Decision thresholding; label sourcing   | Medium (2)| Medium (2) | Medium (2)| 6 – High        | Creates structural barriers to entry |

> **Scoring** = Severity × Likelihood × Relevance  
> Priority scale:
> - 7–9: Critical – requires immediate mitigation  
> - 5–6: High – address post-launch or with additional controls  
> - 3–4: Medium – monitor  
> - 1–2: Low – optional monitoring

---

## 4. Case Study: Income Predictor for Loan Pre-Approval

**System description:**  
A predictive model estimates a user’s income based on self-reported attributes (e.g., occupation, education, location). If income exceeds a predefined threshold, a loan is offered without further documentation.

**Relevance of historical context:**  
- Users with informal or non-traditional jobs (e.g., delivery workers, artisans) are often penalized.  
- Regions historically marginalized (e.g., peri-urban zones) may be treated as higher risk.  
- Educational level is treated as a neutral signal of earnings, despite structural gaps in access.

**Implications:**  
Without historical awareness, this system risks creating a high-tech version of redlining and reinforcing occupational and regional disadvantage.

---

## 5. Implementation Process (Usage Guide)

### Step 1: Domain Research  
- Reviewed academic literature and course readings (e.g., *Fairness and Machine Learning*, unit documents).  
- Identified financial exclusion patterns tied to race, gender, and informality.

### Step 2: Questionnaire Completion  
- Applied the structured questions directly to the loan predictor use case.  
- Answered based on contextual knowledge of Latin American financial systems and documented discrimination.

### Step 3: Risk Classification  
- Scored each historical pattern based on severity, likelihood, and relevance.  
- Prioritized risks that reflect deep structural exclusions — e.g., redlining via proxies.

### Step 4: Documentation and Integration  
- Produced this markdown file as documentation.  
- Findings will feed into:
  - Selection of fairness definitions (e.g., equal opportunity, demographic parity)  
  - Design of bias mitigation interventions  
  - Audit planning and stakeholder communication

---

## References

- Barocas, S., Hardt, M., & Narayanan, A. (2023). *Fairness and Machine Learning*  
- AI Fairness Course, Unit 1: Historical & Societal Foundations  
- Noble, S. (2018). *Algorithms of Oppression*  
- Data & Society reports on financial AI and social inequality  
- O'Neil, C. (2016). *Weapons of Math Destruction*

