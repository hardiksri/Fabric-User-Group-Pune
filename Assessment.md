# Microsoft Fabric Data Agent Workshop Assessment

## Overview

This is a hands-on assessment for the Microsoft Fabric Data Agent workshop. Participants must improve a Power BI semantic model, prepare it for AI, publish it, configure a Fabric Data Agent, validate generated answers, troubleshoot inaccuracies, and use Code Interpreter for advanced analysis.

Use one of the two workshop semantic models:

- **Set A — UrbanCart Semantic Model**
- **Set B — HR Semantic Model**

The two sets assess the same skills with different business domains.

## Assessment format

- **10 core questions**
- **100 marks** — 10 marks per question
- **3 optional advanced challenges**
- Evidence is mandatory. A correct-looking Data Agent response without validation is not sufficient for full marks.

### Evidence expected

Participants should capture relevant evidence such as:

- Power BI Model view screenshots
- TMDL before/after snippets
- Measure definitions
- Object descriptions
- Prep for AI screenshots
- Verified Answer configuration
- Fabric Data Agent configuration
- Prompts and responses
- Generated DAX / run steps
- Before-and-after troubleshooting evidence
- Code Interpreter Python and generated visuals

---

# Set A — UrbanCart

## Q1 — Validate the data model and relationships
**Level:** Beginner  
**Marks:** 10

Inspect the complete UrbanCart semantic model before making AI changes.

Tasks:
1. Identify fact and dimension tables.
2. Confirm the grain of the main fact tables.
3. Review relationship cardinality and filter direction.
4. Check whether required business keys exist on both sides of each relationship.
5. Build any genuinely missing key needed to support a valid relationship.
6. Check for ambiguous paths, inappropriate many-to-many relationships, disconnected business tables, or incorrect active relationships.
7. Record any suspicious or missing relationship you discover.
8. **Do not repair the seeded workshop relationship defect yet** — keep it unchanged for the later Data Agent troubleshooting exercise in Q9.

**Evidence:** Model-view snapshot, identified anomalies, and any key-building work completed. Preserve evidence of the seeded relationship defect for Q9.

---

## Q2 — Make the semantic model business friendly
**Level:** Beginner → Intermediate  
**Marks:** 10

Improve metadata so both business users and AI can understand the model.

Tasks:
1. Rename vague or technical table names into business-friendly names where appropriate.
2. Rename unclear columns and measures.
3. Hide housekeeping fields, surrogate keys, ETL columns, technical flags, and other fields users should not query directly.
4. Add meaningful descriptions to important tables, columns, and measures.
5. Ensure measure names communicate the business calculation clearly.
6. Preserve technical fields required for relationships even when hidden.

**Hint:** Use **TMDL + Copilot** to accelerate bulk renaming, hiding, and description authoring.

**Evidence:** TMDL before/after snippet and Model/Data pane snapshot.

---

## Q3 — Build key KPIs, report visuals, and Verified Answers
**Level:** Intermediate  
**Marks:** 10

Create a small governed KPI layer and use it to establish trusted answers.

Create at least **4 business KPIs**, for example:
- Total Sales
- Total Orders
- Average Order Value
- Return Rate
- Units Sold

Tasks:
1. Create/review the DAX measures.
2. Build at least three useful report visuals using governed measures.
3. Give visuals descriptive titles.
4. Select at least two high-value business questions and configure them as **Verified Answers**.
5. Add multiple natural-language trigger variations for each Verified Answer.
6. Validate that the Verified Answer returns the same governed result as the report.

**Evidence:** KPI definitions, report-page snapshot, Verified Answer configuration and successful test.

---

## Q4 — Prep for AI: simplify the AI Data Schema
**Level:** Intermediate  
**Marks:** 10

Configure **Prep for AI → AI Data Schema** so the AI sees only the business objects needed for the workshop use cases.

Tasks:
1. Select only relevant tables, columns, and governed measures.
2. Remove unnecessary technical fields from the AI-visible schema.
3. Prefer measures over raw additive columns where business logic exists.
4. Ensure Product, Customer, Store, Channel, Promotion, Date, Sales and Returns are represented only as needed.
5. Explain at least three objects you intentionally excluded and why.

**Evidence:** AI Data Schema screenshot and brief rationale.

---

## Q5 — Prep for AI: add semantic-model AI Instructions
**Level:** Advanced  
**Marks:** 10

Use the workshop **Semantic Model AI Instruction Framework** to add business logic to Prep for AI.

Your instructions should cover relevant topics such as:
- Purpose and supported scope
- Governed KPI / measure rules
- Sales and return terminology
- Date behavior and comparison rules
- Product, Store and Channel distinctions
- Filter preservation
- Ambiguous terminology
- Unsupported questions
- Validation expectations

Test at least one question **before and after** adding AI Instructions and explain the change.

> Keep semantic-model-specific query guidance here in Prep for AI. Do not rely on Data Agent-level instructions to fix DAX generation for the semantic model.

**Evidence:** AI Instructions and before/after test.

---

## Q6 — Publish and configure the Fabric Data Agent
**Level:** Intermediate → Advanced  
**Marks:** 10

Publish the improved semantic model to Power BI/Fabric and configure a Fabric Data Agent.

Tasks:
1. Publish the semantic model/report to the assigned workspace.
2. Confirm the published semantic model is accessible.
3. Create or open the workshop Data Agent.
4. Add the Power BI semantic model as a data source.
5. Select only the appropriate semantic-model tables/source scope where applicable.
6. Confirm the agent can retrieve a basic governed result.

**Evidence:** Published model and Data Agent configuration screenshots.

---

## Q7 — Add Data Agent instructions using the workshop framework
**Level:** Advanced  
**Marks:** 10

Use the workshop **Data Agent Instruction Framework** to control agent-wide behavior.

Include instructions for:
- Overall purpose and supported domain
- Routing to the semantic model
- Preserving the user’s intent and filters
- Asking clarifying questions when a request is materially ambiguous
- Response formatting
- Avoiding invented data
- Validation / explainability expectations
- When to use Code Interpreter
- How to handle unsupported questions

Do **not** duplicate semantic-model business rules that belong in Prep for AI.

**Evidence:** Data Agent instruction text and one test showing the intended behavior.

---

## Q8 — Ask progressively harder questions and verify every answer
**Level:** Advanced  
**Marks:** 10

Create a test pack of at least **6 questions** from simple to complex.

Suggested progression:
1. What are total sales?
2. Show sales by channel.
3. What are the top five products by sales?
4. Compare sales with the previous period.
5. Show sales and return rate by customer or customer segment.
6. Which customers or customer segments have high sales but unusually high return rates?

At least one test must deliberately use **Customer together with Sales and/or Returns** so the seeded relationship problem can surface before Q9.

For every question:
- Review the response.
- Review generated DAX / run steps where available.
- Confirm the correct measures, dimensions, filters and date context were used.
- Validate important numbers against Power BI.

**Evidence:** Test matrix containing Prompt, Expected Logic, Agent Result, Validation Result, Pass/Fail.

---

## Q9 — Diagnose the seeded Customer relationship failure, fix it, and retest
**Level:** Expert  
**Marks:** 10

The UrbanCart workshop model contains an **intentional relationship defect** designed to produce an inaccurate or misleading Data Agent answer when Customer attributes are used with Sales and Returns.

Start with a question such as:

> Show Total Sales and Return Rate by Customer Segment.

or

> Which customers have the highest sales and return rates?

Tasks:
1. Ask the question **before repairing the model** and capture the answer.
2. Inspect the generated DAX / run steps and compare the result with Power BI.
3. Trace the issue back to the semantic model rather than trying to solve it only with prompt wording.
4. Identify the missing Customer filtering path to the relevant fact table(s).
5. Restore the correct Customer relationship(s) using the appropriate key, cardinality and filter direction.
6. Refresh/save and republish the corrected semantic model as required.
7. Ask the **exact same question** again.
8. Compare the before/after result and prove that Customer now filters Sales and Returns correctly.
9. Explain why model repair is a more durable fix than adding an AI instruction to compensate for a broken relationship.

**Evidence:** Broken-model screenshot, incorrect response, generated-query/run-step evidence, relationship repair, corrected model screenshot, republished/retested answer, and before/after comparison.

---

## Q10 — Enable Code Interpreter and perform visual analytical reasoning
**Level:** Expert  
**Marks:** 10

Add the **Code Interpreter** tool to the Data Agent and use it for analysis that goes beyond a basic aggregation.

Example prompt:

> Analyze monthly Sales and Return Rate by Channel. Create an appropriate visualization, identify unusual periods, and test whether Sales and Return Rate are correlated. Explain the result without implying causation.

Tasks:
1. Confirm the semantic model retrieves the governed input data.
2. Let Code Interpreter perform the advanced calculation/analysis.
3. Generate at least one visualization.
4. Inspect the Python code, inputs and outputs in run steps.
5. Compare the generated visual/values with a relevant Power BI visual or governed result.
6. Explain which work was performed by the semantic model/Data Agent and which work was performed by Python.

**Evidence:** Prompt, run steps, generated Python, output visual and validation note.

---

# Set B — HR

Use the same ten tasks, but apply them to the HR semantic model and workforce terminology.

## Q1 — Validate the HR data model and relationships
Inspect the headcount, payroll, performance, requisition and termination facts; validate their individual grains and shared dimensions such as Employee, Department, Job, Location and Date. Create any genuinely missing relationship key required for a valid star-style model.

Record suspicious or missing relationships, but **do not repair the seeded Department-to-Headcount relationship defect yet**. It is intentionally preserved for the troubleshooting exercise in Q9.

**Evidence:** Model-view snapshot, identified anomalies, and any key-building work completed.

## Q2 — Make the HR semantic model business friendly
Rename technical/vague HR objects, hide housekeeping and technical keys, and add descriptions to important tables, columns and measures. Use TMDL + Copilot where helpful.

**Evidence:** TMDL before/after plus model snapshot.

## Q3 — Build HR KPIs, visuals, and Verified Answers
Create at least four governed KPIs, for example:
- Headcount / Month-end Headcount
- Total Payroll
- Terminations
- Turnover Rate
- Open Requisitions
- Average Performance Rating

Build three visuals and create at least two Verified Answers from high-value HR questions.

**Evidence:** Measures, visuals and Verified Answers.

## Q4 — Prep for AI: simplify the HR AI Data Schema
Expose only fields needed for aggregated workforce analysis. Remove unnecessary employee-level identifiers, technical keys and implementation fields from the AI-visible schema.

**Evidence:** AI Data Schema screenshot and rationale.

## Q5 — Prep for AI: add HR semantic-model AI Instructions
Use the workshop framework to define business terminology and calculation rules such as:
- Headcount vs month-end headcount
- Monthly snapshot behavior
- Termination / turnover terminology
- Payroll interpretation
- Performance rating interpretation
- Date-period rules
- Governed measure preference

Explicitly prevent the AI from simply summing monthly headcount snapshots across months.

**Evidence:** AI Instructions and before/after test.

## Q6 — Publish and configure the Fabric Data Agent
Publish the HR model, add it to a Fabric Data Agent and confirm a basic governed HR question works.

**Evidence:** Service and Data Agent configuration screenshots.

## Q7 — Add Data Agent instructions using the workshop framework
Add agent-wide instructions for routing, clarification, response formatting, scope, validation, unsupported requests, privacy-aware aggregate responses, and Code Interpreter usage. Keep model-specific DAX logic in Prep for AI.

**Evidence:** Agent instructions and test.

## Q8 — Ask progressively harder HR questions and verify them
Test at least six questions, for example:
1. What was last month's headcount?
2. Show headcount by department.
3. How many terminations occurred by location?
4. Compare turnover by department.
5. Which departments have rising requisitions while headcount is declining?
6. How did average performance rating and turnover move over time at department level?

At least one test must deliberately use **Department with Headcount** so the seeded relationship problem can be observed before Q9.

Validate measures, dimensions, dates, filters and generated DAX.

**Evidence:** Prompt-validation matrix.

## Q9 — Diagnose the seeded Department-to-Headcount failure, fix it, and retest
The HR workshop model contains an **intentional relationship defect** affecting Department-level Headcount analysis.

Start with a question such as:

> Show last month's Headcount by Department.

or

> Which departments have the highest Headcount?

Tasks:
1. Ask the question **before repairing the model** and capture the answer.
2. Inspect the generated DAX / run steps and validate the numbers in Power BI.
3. Determine whether the problem is in the prompt, measure logic, AI configuration, or model relationship.
4. Trace the issue to the missing Department filtering path into the Headcount fact.
5. Restore the Department-to-Headcount relationship with the correct key, cardinality and filter direction.
6. Refresh/save and republish the model as required.
7. Ask the **exact same question** again.
8. Compare the before/after results and prove Department now filters Headcount correctly.
9. Explain why fixing the semantic model is preferable to masking the problem with Data Agent instructions.

**Evidence:** Broken-model screenshot, incorrect response, generated-query/run-step evidence, relationship repair, corrected model screenshot, and before/after answer validation.

## Q10 — Enable Code Interpreter and perform visual workforce analysis
Example prompt:

> Analyze monthly Headcount, Terminations and Requisitions by Department. Create appropriate visuals, identify unusual periods, and test whether changes in Terminations are associated with changes in Headcount. Do not rank individual employees or make employment recommendations.

Inspect generated Python and validate the input metrics against the semantic model.

**Evidence:** Run steps, Python, visualization and conclusion.

---

# Optional Advanced Challenges

## Challenge 11 — Security and access validation
Validate that the Data Agent respects the access/security behavior expected for the semantic model. If RLS/OLS is present, test with an appropriate user context and document what should and should not be visible.

## Challenge 12 — Build an accuracy benchmark
Create a reusable benchmark of **10 golden questions** with expected measures, dimensions, filters and results. Run them after each major Prep for AI/model change and calculate an accuracy pass rate.

Suggested columns:

| Question | Expected Measure | Expected Dimension | Expected Filter/Date Logic | Actual Result | Pass/Fail | Notes |
|---|---|---|---|---|---|---|

## Challenge 13 — Production-readiness review
Create a one-page readiness summary covering:
- Model quality
- Metadata quality
- AI Data Schema
- AI Instructions
- Verified Answers
- Data Agent instructions
- Accuracy benchmark
- Security/access
- Known limitations
- Code Interpreter use cases

Give the solution a final status of **Ready**, **Ready with Conditions**, or **Not Ready** and justify the decision.

---

# Facilitator Scoring Guide

Each core question is worth 10 marks:

- **4 marks — Technical correctness**: correct model/configuration/change
- **3 marks — Evidence and validation**: participant proves the result
- **2 marks — Reasoning**: participant explains why the approach is correct
- **1 mark — Communication**: clear, business-friendly explanation

## Critical rule

Do not award full marks simply because the Data Agent produced an answer.

Participants should demonstrate the chain:

**Question → Semantic Model / Prep for AI → Generated Query → Result → Validation → Fix/Interpretation**

For Code Interpreter:

**Question → Governed Data Retrieval → Code Interpreter → Python / Visual → Validation → Business Interpretation**

---

# Facilitator Notes

- AI Data Schema, AI Instructions and Verified Answers should be configured through **Prep for AI** for Power BI semantic models.
- Semantic-model-specific instructions should not be placed only at the Data Agent level; the semantic-model DAX generation path relies on the semantic model metadata and Prep for AI configuration.
- Data Agent-level instructions are best used for agent-wide routing, clarification, response behavior, common terminology across sources, formatting and tool-use guidance.
- Code Interpreter is an advanced tool for Python-based analysis and visualizations over data retrieved by the Data Agent. Participants should inspect its generated code and validate its inputs/outputs.

---

# Facilitator Seeded Defects

These defects are intentionally present in the workshop PBIX files so participants can experience a realistic Data Agent accuracy failure and repair cycle.

- **UrbanCart:** Customer filtering relationships to **Fact Sales** and **Fact Return** are intentionally removed. The expected failure should surface when Customer attributes are combined with Sales and/or Return metrics.
- **HR:** The **Department → Headcount** relationship is intentionally removed. The expected failure should surface when Headcount is grouped or filtered by Department.

Do not repair these seeded defects during the initial model-review exercise. Preserve them until Q9, where participants must demonstrate **wrong answer → diagnosis → model fix → republish/retest → corrected answer**.
