Weekly Report: LLM Prompt Testing, Evaluation Refinement and Analytics Prompt Expansion
---------------------------------------------------------------------------------------

Date: December 6 to December 12

### Focus Areas

-   Support prompt re testing using refined handbook

-   Scoring rubric tightening and validation

-   Analytics prompt expansion with concrete examples

-   Guidance on proper and improper analytics prompt usage

* * * * *

Overview
--------

This week focused on strengthening the reliability of existing prompt work rather than expanding scope. The emphasis was on validating earlier improvements, making evaluation stricter, and ensuring prompts fail less silently. Instead of adding new use cases, the work aimed to reduce ambiguity and raise the quality bar for both support and analytics prompts.

The goal was to move from "better than before" to "harder to get wrong," especially by improving evaluation discipline and tightening definitions of what counts as a good answer.

* * * * *

Day 1: Review of Prior Results and Test Set Refinement
------------------------------------------------------

### Overview

Started the week by reviewing outcomes from the previous support prompt iteration to ensure only unresolved or borderline issues were carried forward.

### Work Done

-   Reviewed previously logged support prompt failures and filtered out cases already addressed

-   Selected a smaller and more realistic set of support conversations to reduce noise

-   Updated handbook notes to reflect stricter expectations for clarity and resolution

### Result

Established a focused and relevant test set that better represents real support interactions.

* * * * *

Day 2: Second Round of Support Prompt Testing
---------------------------------------------

### Overview

Ran the refined support prompts against the updated conversation set to validate improvements.

### Work Done

-   Executed prompts against realistic support cases including payment issues, ride delays and cancellation confusion

-   Captured responses without manual intervention

-   Flagged responses that sounded correct but lacked concrete next steps

### Result

Confirmed improvement in structure and tone while surfacing subtler failure modes that were previously masked.

* * * * *

Day 3: Scoring Rubric Tightening
--------------------------------

### Overview

Refined the evaluation rubric to prevent superficially polished answers from scoring well.

### Work Done

-   Reduced emphasis on language fluency and increased weight on correctness and actionability

-   Clarified scoring thresholds so high scores require explicit resolution steps

-   Updated rubric definitions directly in the handbook

### Result

Evaluation became more resistant to vague or generic responses, making scores more meaningful.

* * * * *

Day 4: Re Evaluation and Validation
-----------------------------------

### Overview

Validated the tightened rubric by re scoring existing responses.

### Work Done

-   Re scored a subset of support responses using the updated rubric

-   Compared old scores to new scores to verify stricter grading

-   Documented examples of strong versus weak answers with reasoning

### Result

Confirmed that the rubric now penalizes shallow answers and rewards true usefulness.

* * * * *

Day 5: Analytics Prompt Example Expansion
-----------------------------------------

### Overview

Expanded the analytics prompt with a concrete example to anchor model behavior.

### Work Done

-   Selected a small BimRide analytics scenario with clearly defined inputs

-   Added one example input and expected output to the analytics prompt

-   Focused on structure and reasoning flow rather than completeness

### Result

Improved prompt clarity and reduced model guesswork in analytics responses.

* * * * *

Day 6: Analytics Prompt Boundary Definition
-------------------------------------------

### Overview

Defined when the analytics prompt should not be used to avoid misuse.

### Work Done

-   Identified cases where analytics prompts produce misleading or speculative outputs

-   Documented limitations such as incomplete data or real time decision contexts

-   Added a short internal guidance note to the handbook

### Result

Reduced risk of inappropriate prompt usage by clearly documenting boundaries.

* * * * *

Day 7: Consolidation and Review
-------------------------------

### Overview

Reviewed all changes made during the week to ensure consistency and alignment.

### Work Done

-   Reviewed support prompt improvements against initial baselines

-   Ensured scoring rubric, prompts and handbook documentation were aligned

-   Noted minor gaps and follow ups for future refinement

### Result

Ended the week with more reliable prompts, stricter evaluation standards and clearer usage guidance, reinforcing a repeatable improvement process.
