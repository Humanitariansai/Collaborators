# Weekly Report: LLM Prompt Testing, Evaluation, and Analytics

**Date:** November 29 – December 5  
**Focus Areas:**
* Support prompt testing and failure analysis
* Prompt refinement and handbook updates
* LLM answer evaluation using a simple scoring rubric
* Initial analytics prompt drafting for a BimRide use case

---

## Executive Summary
This week focused on applying LLM fundamentals in a practical, controlled environment. The primary goal was to pressure-test existing prompts, observe failure patterns, and establish a repeatable, evidence-based workflow for prompt improvement. Work was intentionally narrowed to support conversations and a preliminary analytics experiment to ensure depth over breadth.

---

## Daily Breakdown

### Day 1: Baseline Testing
**Goal:** Establish a performance baseline using realistic support scenarios.
* **Work Done:** Collected representative cases (ride cancellations, payment issues, delayed pickups, and account access).
* **Process:** Ran raw conversations through existing prompts without any modifications.
* **Result:** Established a "ground truth" baseline of model behavior under realistic conditions.

### Day 2: Failure Pattern Identification
**Goal:** Categorize systematic prompt weaknesses.
* **Work Done:** Analyzed responses for clarity, correctness, tone, and completeness.
* **Common Failures Identified:**
    * **Vague Answers:** Lack of specific resolution.
    * **Constraint Neglect:** Ignoring specific user instructions.
    * **Overconfidence:** Hallucinating policy details.
* **Result:** Documented concrete, repeatable failure patterns to be addressed systematically.

### Day 3: Support Prompt Refinement
**Goal:** Iterative prompt engineering based on Day 2 findings.
* **Work Done:** * Updated system prompts to emphasize **Chain-of-Thought (CoT)** reasoning.
    * Tightened language regarding escalation boundaries and brand tone.
* **Result:** Responses became more structured and actionable with a noticeable reduction in generic "filler" text.

### Day 4: Evaluation via Scoring Rubric
**Goal:** Transition from subjective "vibes" to objective measurement.
* **Scoring Criteria:**
    | Criteria | Description |
    | :--- | :--- |
    | **Correctness** | Is the information factually accurate? |
    | **Clarity** | Is the response easy to understand? |
    | **Tone** | Is the persona helpful and calm? |
    | **Usefulness** | Does it provide a clear next step? |
* **Result:** Qualitative improvements are now backed by quantitative scores, making the iteration process disciplined.

### Day 5: Handbook Updates
**Goal:** Institutionalize knowledge.
* **Work Done:** Added a **Troubleshooting Section** to the LLM Handbook.
* **Content:** Documented "Before vs. After" prompt examples and specific patterns that consistently improved model output.
* **Result:** The handbook now serves as a practical reference for the team.

### Day 6: Analytics Prompt Drafting
**Goal:** Apply support-case learnings to a new domain (BimRide Analytics).
* **Scenario:** Summarizing weekly driver retention trends.
* **Approach:** Drafted system prompts with strict scope limits and specific output structures (e.g., JSON or Markdown tables).
* **Result:** A clean, exploratory draft ready for the same rubric-based testing used in support.

### Day 7: Review & Consolidation
**Goal:** Final alignment check.
* **Work Done:** Side-by-side comparison of baseline vs. refined responses.
* **Outcome:** Confirmed that all prompt iterations were driven by data (failure patterns) rather than intuition.

---

## Key Takeaways
> **Systematic Iteration:** Prompt engineering is more effective when treated as a debugging process (Identify Failure -> Categorize -> Refine -> Evaluate).
>
> **Evidence over Intuition:** Using a scoring rubric removes bias and provides a clear audit trail for why certain prompt structures were chosen.
