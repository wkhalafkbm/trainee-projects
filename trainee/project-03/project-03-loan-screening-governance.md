# Project 3: Loan/Credit Application Screening Tool (with Governance)

**Stack:** watsonx.ai + watsonx.governance  
**Duration:** 2 weeks (platform/lab ramp-up and build, split as needed)  
**Difficulty:** Tier 3 — Advanced

---

## Overview

Build an AI-assisted loan application screening tool that evaluates credit applications and recommends an outcome — approve, refer for manual review, or decline. Then wrap the entire system in a governance layer: track every decision, detect bias in the outcomes, generate explanations for each recommendation, and produce a governance report at the end.

This is the first project in the programme where the *quality of the AI output alone is not enough*. A loan screening tool that is accurate but biased, or accurate but unexplainable, is not deployable — not legally, not ethically, and not practically. This project forces the trainee to confront a question that every AI developer eventually faces: what does it mean to build AI responsibly, and how do you prove it?

The tool uses a foundation model on watsonx.ai for the screening logic. watsonx.governance is used to monitor the model, track decisions, detect fairness issues, and produce a factsheet. By the end of the week, the trainee will have built not just an AI application but a governed one.

---

## What to Build

A working loan screening pipeline with:

1. **Application intake** — accept a structured loan application (applicant details, financial profile) as input
2. **Screening model** — a watsonx.ai foundation model that evaluates the application and returns a recommendation (Approve / Refer / Decline) with a confidence score and a plain-language justification
3. **Explainability layer** — for every decision, produce a human-readable explanation of the key factors that influenced the outcome
4. **Bias detection** — run the model against a test dataset and analyse whether outcomes differ systematically across protected attributes (age group, gender, nationality)
5. **Decision log** — persist every application, recommendation, and explanation to a structured log for audit purposes
6. **watsonx.governance integration** — register the model, track it via a factsheet, and produce a governance report
7. **Human review path** — all Decline and low-confidence Approve decisions must be flagged for human review, not acted on autonomously

---

## Milestones

### Milestone 1 — Understand responsible AI in financial services
- Read about why AI in lending is a regulated domain: what adverse action notices are, what the Central Bank of Kuwait's (CBK) consumer credit regulations require, and why explainability is not optional
- Read about the types of bias that can appear in AI systems: historical bias (the training data reflects past discrimination), representation bias (some groups are underrepresented), and measurement bias (features used as proxies for protected attributes)
- Familiarise yourself with watsonx.governance: what it tracks, what a factsheet is, and what a model card should contain
- Deliverable: a written summary (1 page) of the three types of bias and one example of each from the financial services domain

### Milestone 2 — Build the screening model
- Design the prompt: the model receives a structured application profile and must return a JSON response containing the recommendation, confidence score, and justification
- Define the exact fields in the output schema before writing the prompt
- Test the prompt against the sample applications in this document
- Ensure the model never returns a Decline without a justification that references specific application data — not a generic reason
- Deliverable: a working screening prompt with structured JSON output, tested against at least 10 sample applications

### Milestone 3 — Build the explainability layer and decision log
- Explainability: for each decision, produce a second output that lists the top factors that influenced the outcome in plain language a non-expert can read (e.g. "Existing monthly debt of KWD 300 represents 37.5% of your net salary, approaching the CBK's 40% Debt Burden Ratio limit for expat applicants")
- Decision log: write every application + recommendation + explanation to a structured log file (JSON Lines format is suitable)
- Test the explanation quality: would a loan officer be able to use this explanation to have a meaningful conversation with the applicant about why their application was referred?
- Deliverable: working explainability output for all three decision types, and a populated decision log after running the full sample set

### Milestone 4 — Bias detection and fairness analysis
- Run the screening model against the full sample dataset (at least 30 applications)
- Segment outcomes by gender, age group, and nationality — calculate approval rates, referral rates, and decline rates for each segment
- Identify whether any group has a meaningfully different outcome distribution compared to others
- If a disparity is found, investigate the cause: is it a legitimate difference in the financial profiles, or is the model using a proxy attribute?
- Attempt at least one mitigation and re-run to see whether it improves the disparity
- Deliverable: a bias analysis report (can be a markdown file or spreadsheet) containing outcome distributions by segment, a finding, and a documented mitigation attempt

### Milestone 5 — watsonx.governance integration and final report
- Register the model in watsonx.governance
- Populate the model factsheet: intended use, training data description (or in this case, prompt design description), known limitations, fairness findings, and recommended human oversight steps
- Configure basic monitoring: log inputs and outputs so drift could be detected over time
- Write the governance report (see Acceptance Criteria for required contents)
- Deliverable: a completed factsheet and a governance report

---

## Key Concepts to Understand

### Why Lending AI is Different

Most AI applications fail gracefully — a bad movie recommendation is annoying, not harmful. A bad loan decision has material consequences for a real person: it can prevent them from buying a home, starting a business, or managing a financial emergency. This asymmetry changes the design requirements:

- Decisions must be **explainable** to the person affected, not just accurate in aggregate
- The system must be **auditable** — every decision must be traceable to the inputs and the model version that produced it
- Certain factors **must not influence outcomes** regardless of their predictive power (gender, religion, national origin). In Kuwait specifically, nationality (Kuwaiti national vs. expat) is a dimension that requires careful handling — while the CBK permits different Debt Burden Ratio (DBR) caps for nationals and expats, nationality must not be used as a blanket discriminator beyond what the DBR rules justify
- A human must be **reachable** — there must be a path for the applicant to have their case reviewed by a person

None of these requirements come from the model itself. They come from the system design around it.

### Types of Bias

**Historical bias** occurs when the model learns patterns from data that reflects past discriminatory decisions. If a bank historically denied loans to applicants from certain postcodes, and postcode is a feature, the model will replicate that discrimination even if it was wrong to begin with.

**Representation bias** occurs when some groups are underrepresented in the evaluation data. A model tested primarily on one demographic may perform poorly on others without anyone noticing, because the poorly-served group is a small portion of the test set.

**Proxy bias** occurs when a feature that seems neutral is actually correlated with a protected attribute. In lending, "years at current address" can be a proxy for age; "employer type" can correlate with gender. Removing the protected attribute does not remove the bias if proxies remain.

### Fairness Metrics

Fairness is not a single number — it is a set of properties that are mathematically incompatible with each other in many real-world scenarios. The trainee should understand at least two:

**Demographic parity:** the approval rate should be the same across groups. Simple, but this ignores legitimate differences in financial profiles.

**Equalised odds:** the true positive rate (correctly approving creditworthy applicants) and false positive rate (incorrectly approving non-creditworthy applicants) should be the same across groups. More sophisticated, because it conditions on the actual creditworthiness of the applicant.

The trainee does not need to implement these formally — they need to understand why demographic parity alone is insufficient, and why the choice of fairness metric is itself a value judgement.

### Explainability vs. Interpretability

These are often used interchangeably but mean different things:

- **Interpretability:** you can look at the model and understand how it works (a decision tree is interpretable; a foundation model is not)
- **Explainability:** for a specific decision, you can produce a post-hoc explanation of why that outcome was reached

Foundation models are not interpretable, but they can be prompted to produce explanations. The risk is that the explanation is a plausible-sounding rationalisation rather than a faithful account of the model's reasoning. The trainee should understand this limitation and note it in their governance report.

### Model Factsheets

A factsheet is a structured document that captures everything a decision-maker needs to know before deploying or trusting an AI model:

- What the model is designed to do (intended use)
- What data it was trained on or prompted with
- Known limitations and failure modes
- Fairness analysis results
- Recommended oversight and escalation procedures
- Who is accountable for the model's outputs

watsonx.governance provides tooling to create and maintain factsheets. The trainee should treat it not as a compliance checkbox but as the document that would need to exist if a regulator asked to audit the system.

### The Human Review Path is Not Optional

In a lending context, an AI system that makes final decisions autonomously — especially Decline decisions — is not compliant with financial services regulations in most jurisdictions. The human review path is not a fallback for low confidence; it is a structural requirement. Every Decline decision must be reviewable by a human, and that review must be accessible to the applicant.

The trainee should design the system so that:
- Decline decisions produce an output packet for a human reviewer, not a final rejection notice
- The human reviewer receives the full application, the model's recommendation, the explanation, and a clear interface to override
- The applicant is never told "the computer said no" — they are told their application is under review

---

## Acceptance Criteria

### For the trainee — the system must:
- [ ] Produce a recommendation (Approve / Refer / Decline), confidence score, and plain-language justification for every application
- [ ] Flag all Decline decisions and any Approve decisions below 0.75 confidence for human review — these must not be treated as final
- [ ] Include a structured decision log covering all applications processed during testing
- [ ] Include a bias analysis report covering outcome distributions by gender, age group, and nationality, at least one finding, and a documented mitigation attempt
- [ ] Include a completed watsonx.governance factsheet for the model
- [ ] Include a governance report (see structure below)

### Governance Report — Required Contents
The governance report is the primary proof-of-learning artefact for this project. It must cover:

1. **Model description:** what the model does, what inputs it takes, what outputs it produces
2. **Intended use and out-of-scope use:** where this model should and should not be used
3. **Fairness analysis:** outcome distributions by protected attribute, methodology used, findings
4. **Bias finding:** at least one identified disparity, its likely cause, and the mitigation attempted
5. **Explainability approach:** how explanations are generated and their limitations
6. **Human oversight design:** which decisions require human review and why
7. **Known limitations:** what the model cannot reliably do
8. **Recommendations:** what would need to be true before this system could be deployed in a real lending context

---

## Sample Application Dataset

Use these applications to build and test the pipeline. They include a range of financial profiles and edge cases.

All income and loan figures are in Kuwaiti Dinar (KWD). The CBK's Debt Burden Ratio (DBR) cap is 40% of monthly net salary for expats and 50% for Kuwaiti nationals — the model should be aware of this regulatory difference but must not use nationality as a blanket approval or decline signal beyond what the DBR calculation justifies.

---

**Application 001**
```json
{
  "applicant_id": "A001",
  "age": 34,
  "gender": "Female",
  "nationality": "Kuwaiti",
  "employment_status": "Full-time employed",
  "employer_type": "Government",
  "years_employed": 6,
  "monthly_net_salary_kwd": 1200,
  "monthly_expenses_kwd": 320,
  "existing_debt_monthly_kwd": 180,
  "loan_amount_requested_kwd": 18000,
  "loan_purpose": "Home renovation",
  "credit_score": 740,
  "previous_defaults": 0
}
```
Expected lean: Approve

---

**Application 002**
```json
{
  "applicant_id": "A002",
  "age": 27,
  "gender": "Male",
  "nationality": "Expat",
  "employment_status": "Full-time employed",
  "employer_type": "Private sector",
  "years_employed": 1.5,
  "monthly_net_salary_kwd": 800,
  "monthly_expenses_kwd": 380,
  "existing_debt_monthly_kwd": 210,
  "loan_amount_requested_kwd": 8000,
  "loan_purpose": "Vehicle purchase",
  "credit_score": 620,
  "previous_defaults": 1
}
```
Expected lean: Refer (prior default and DBR is borderline at 40%)

---

**Application 003**
```json
{
  "applicant_id": "A003",
  "age": 52,
  "gender": "Male",
  "nationality": "Kuwaiti",
  "employment_status": "Full-time employed",
  "employer_type": "Government",
  "years_employed": 22,
  "monthly_net_salary_kwd": 2400,
  "monthly_expenses_kwd": 600,
  "existing_debt_monthly_kwd": 350,
  "loan_amount_requested_kwd": 35000,
  "loan_purpose": "Home purchase",
  "credit_score": 780,
  "previous_defaults": 0
}
```
Expected lean: Approve

---

**Application 004**
```json
{
  "applicant_id": "A004",
  "age": 24,
  "gender": "Female",
  "nationality": "Expat",
  "employment_status": "Full-time employed",
  "employer_type": "Private sector",
  "years_employed": 0.75,
  "monthly_net_salary_kwd": 450,
  "monthly_expenses_kwd": 220,
  "existing_debt_monthly_kwd": 80,
  "loan_amount_requested_kwd": 3500,
  "loan_purpose": "Education",
  "credit_score": 590,
  "previous_defaults": 0
}
```
Expected lean: Refer (borderline — short employment history, but no defaults and legitimate purpose)

---

**Application 005**
```json
{
  "applicant_id": "A005",
  "age": 44,
  "gender": "Female",
  "nationality": "Kuwaiti",
  "employment_status": "Full-time employed",
  "employer_type": "Private sector",
  "years_employed": 11,
  "monthly_net_salary_kwd": 3200,
  "monthly_expenses_kwd": 900,
  "existing_debt_monthly_kwd": 1100,
  "loan_amount_requested_kwd": 50000,
  "loan_purpose": "Investment property",
  "credit_score": 680,
  "previous_defaults": 2
}
```
Expected lean: Decline (existing debt already at 34% DBR, two prior defaults)

---

**Application 006**
```json
{
  "applicant_id": "A006",
  "age": 31,
  "gender": "Male",
  "nationality": "Expat",
  "employment_status": "Full-time employed",
  "employer_type": "Oil & Gas",
  "years_employed": 4,
  "monthly_net_salary_kwd": 1600,
  "monthly_expenses_kwd": 420,
  "existing_debt_monthly_kwd": 200,
  "loan_amount_requested_kwd": 12000,
  "loan_purpose": "Vehicle purchase",
  "credit_score": 710,
  "previous_defaults": 0
}
```
Expected lean: Approve

---

**Application 007**
```json
{
  "applicant_id": "A007",
  "age": 61,
  "gender": "Female",
  "nationality": "Expat",
  "employment_status": "Full-time employed",
  "employer_type": "Private sector",
  "years_employed": 18,
  "monthly_net_salary_kwd": 950,
  "monthly_expenses_kwd": 280,
  "existing_debt_monthly_kwd": 90,
  "loan_amount_requested_kwd": 7000,
  "loan_purpose": "Home renovation",
  "credit_score": 720,
  "previous_defaults": 0
}
```
Expected lean: Refer (age relative to loan term is worth flagging — financially this is sound, so watch for age bias)

---

**Application 008**
```json
{
  "applicant_id": "A008",
  "age": 29,
  "gender": "Male",
  "nationality": "Expat",
  "employment_status": "Unemployed",
  "employer_type": "N/A",
  "years_employed": 0,
  "monthly_net_salary_kwd": 0,
  "monthly_expenses_kwd": 250,
  "existing_debt_monthly_kwd": 300,
  "loan_amount_requested_kwd": 4000,
  "loan_purpose": "Debt consolidation",
  "credit_score": 510,
  "previous_defaults": 3
}
```
Expected lean: Decline

---

Add at least 22 more applications of your own, ensuring a balanced distribution across gender, age groups (under 30, 30–50, over 50), and nationality (Kuwaiti / Expat) before running your bias analysis.

---

## Bias Analysis Guide

When you have processed your full dataset, calculate the following for each group:

**By gender (Male / Female):**
- Approval rate
- Referral rate
- Decline rate

**By age group (Under 30 / 30–50 / Over 50):**
- Approval rate
- Referral rate
- Decline rate

**By nationality (Kuwaiti / Expat):**
- Approval rate
- Referral rate
- Decline rate

For the nationality dimension, note that some disparity is expected and legitimate: the CBK's DBR caps differ (50% for nationals, 40% for expats), which means expats with the same salary will qualify for smaller loans. The question is whether the model's outcome disparity is proportional to what the DBR rules alone explain, or whether it is larger — suggesting nationality is being weighted beyond its regulatory justification.

Look for a disparity of more than 10 percentage points in approval rates between any two groups that is not fully explained by financial profile differences. If you find one, ask:
1. Is it explained by legitimate differences in the financial profiles or applicable regulatory caps for those groups?
2. Or does the model appear to be treating similar financial profiles differently based on the protected attribute alone?

To test question 2, find two applications with near-identical financial profiles but different values for the protected attribute. If the model recommends different outcomes, that is a proxy bias signal worth investigating.

---

## Common Pitfalls to Watch For

- **Confusing correlation with bias:** if older applicants in your dataset happen to have higher incomes, the model will approve them more often — but that is not bias, it is responding to the financial data. Bias is when the protected attribute influences the outcome beyond what the financial data justifies.
- **Explanations that don't reflect the decision:** a model can produce a confident-sounding explanation that does not actually correspond to why it made the decision it did. Test this by asking the model to explain a decision and then modifying a single input — does the explanation update accordingly?
- **Treating the factsheet as a formality:** trainees who fill in the factsheet quickly without honest reflection produce boilerplate. The mentor should probe the limitations section specifically — if it says "none known," that is almost certainly wrong.
- **Setting an autonomy boundary that is too wide:** a trainee who configures the system to approve applications automatically is optimising for convenience, not responsible deployment. Every Decline and every low-confidence decision must pass through a human.
- **Not documenting the mitigation:** saying "I adjusted the prompt and the bias went away" is not a mitigation — it is an observation. The trainee must document what they changed, why they expected it to help, and what the outcome distribution looked like after the change.

---

## Stretch Goals (for more experienced trainees)

- Implement a **counterfactual explanation**: for every Decline, generate a statement of the form "If your credit score were X instead of Y, this application would have been referred rather than declined" — this is a form of explanation that is directly actionable for the applicant
- Add an **adverse action notice generator**: produce a formal letter for Decline decisions that meets the plain-language explanation requirements of the Central Bank of Kuwait's consumer credit guidelines
- Implement **model drift simulation**: process the same application twice with slightly different prompt wording and compare outcomes — document how sensitive the model is to prompt changes and what this means for production stability
- Explore **watsonx.governance's automated bias detection**: move beyond manual spreadsheet analysis and use the platform's built-in fairness metrics tooling

---

## Resources

- watsonx.governance documentation: model factsheets, monitoring configuration, fairness metrics
- IBM AI Fairness 360 (AIF360) — open-source toolkit for bias detection and mitigation, useful for understanding the underlying metrics
- "Fairness and Machine Learning" (Barocas, Hardt, Narayanan) — free online textbook, Chapters 1–3 are relevant to this project
- "Model Cards for Model Reporting" (Mitchell et al., 2019) — the paper that established model cards as a governance practice
