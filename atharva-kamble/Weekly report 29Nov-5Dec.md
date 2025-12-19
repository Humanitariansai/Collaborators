Weekly Report: LLM Prompt Testing, Evaluation and Analytics Prompt Drafting
===========================================================================

**Date:** November 29 to December 5

**Focus Areas:**

*   Support prompt testing and failure analysis
    
*   Prompt refinement and handbook updates
    
*   LLM answer evaluation using a simple scoring rubric
    
*   Initial analytics prompt drafting for a BimRide use case
    

Overview
--------

This week focused on applying LLM fundamentals in a practical and controlled way rather than learning new theory.The goal was to pressure test existing prompts, observe failure patterns, and build a repeatable way to improve prompt quality using evaluation instead of intuition.

The work stayed intentionally narrow to avoid overload.Support conversations were used as the primary testing ground, followed by a small analytics prompt experiment to extend the same thinking into a different use case.

Day 1: Support Conversation Selection and Baseline Prompt Testing
-----------------------------------------------------------------

### Overview

Started by selecting a small set of realistic support scenarios to test against the current prompts.

### Work Done

*   Collected representative support cases such as ride cancellation issues, payment confusion, delayed pickup complaints and account access problems
    
*   Ran these conversations through the existing support prompts without modification
    
*   Captured raw model responses exactly as generated
    

### Result

Established a clear baseline of how the current prompts behave under realistic conditions, without bias or tuning.

Day 2: Failure Pattern Identification
-------------------------------------

### Overview

Focused on identifying where and why the support prompts perform poorly.

### Work Done

*   Reviewed responses for clarity, correctness, tone and completeness
    
*   Flagged common failure modes such as vague answers, missed constraints, overconfidence and lack of actionable steps
    
*   Grouped failures into categories instead of treating each response as a one off issue
    

### Result

Prompt weaknesses were no longer abstract.They were documented as concrete, repeatable failure patterns that can be fixed systematically.

Day 3: Support Prompt Refinement
--------------------------------

### Overview

Refined the support prompts based directly on observed failures rather than guesswork.

### Work Done

*   Adjusted system prompt instructions to emphasize step by step reasoning and clear resolution paths
    
*   Tightened language around tone and escalation boundaries
    
*   Re tested the same support conversations using the updated prompts
    

### Result

Responses became more structured, calmer and more actionable, with fewer hallucinated or overly generic answers.

Day 4: Evaluation Using Scoring Rubric
--------------------------------------

### Overview

Applied a simple evaluation framework to make quality measurable instead of subjective.

### Work Done

*   Defined a lightweight scoring rubric covering correctness, clarity, tone and usefulness
    
*   Scored both original and refined responses using the same rubric
    
*   Wrote short notes explaining why a response scored high or low
    

### Result

Prompt improvements could now be justified with evidence rather than intuition, making iteration more disciplined.

Day 5: Handbook Updates and Troubleshooting Section
---------------------------------------------------

### Overview

Captured learnings in the LLM handbook so progress does not stay only in memory.

### Work Done

*   Added a troubleshooting section describing common support prompt failures and fixes
    
*   Documented example bad answers versus improved answers
    
*   Recorded prompt patterns that consistently improved outcomes
    

### Result

The handbook evolved into a practical reference instead of a theoretical notes file.

Day 6: Analytics Use Case Selection and Prompt Drafting
-------------------------------------------------------

### Overview

Extended the same prompt thinking into a small analytics use case.

### Work Done

*   Selected a simple analytics scenario such as summarizing weekly driver retention trends
    
*   Drafted a first version of system and user prompts focused on clarity, scope limits and output structure
    
*   Avoided over optimization and treated this as an exploratory draft
    

### Result

Created a clean starting point for analytics prompts that can later be evaluated using the same rubric approach.

Day 7: Review and Consolidation
-------------------------------

### Overview

Reviewed the week’s work and checked alignment with the original goals.

### Work Done

*   Compared baseline and refined support responses side by side
    
*   Confirmed that prompt changes were driven by observed failures
    
*   Reviewed handbook completeness and noted gaps for future updates
    

### Result

The week ended with tested prompts, documented learnings and a repeatable improvement process instead of scattered experimentation.
