# Weekly Report: RAG Prototype, Prompt Evaluation and LLM Logging  
**Date:** 15 to 21 November  
**Topics Covered:**  
1. RAG Prototype for a Narrow Use Case  
2. Evaluation Rubric Applied to Real LLM Answers  
3. Prompt Design and Iteration for a Concrete Workflow  
4. Logging for RAG Requests and Responses  
5. Updates to the LLM Handbook  

---

## Overview  

This week was about stopping theory and actually putting LLM concepts to work.  
Instead of reading more material, I built a small retrieval augmented generation prototype, tested it under a real workflow, and forced my evaluation rubric to prove that it is useful instead of sitting in a document.

The focus was simple and ruthless  
take one narrow use case, wire up retrieval, capture logs, score outputs, and update the LLM handbook with what actually worked and what broke.

---

## Day 1: RAG Use Case Selection and Scope  

### Overview  

Started by choosing a very specific use case so the RAG work did not explode in scope.

### Work Done  

1. Picked a narrow scenario  
   support style question answering over a small internal knowledge set.  
2. Defined what a good answer means for this use case  
   must be grounded in the provided text, concise and directly useful.  
3. Listed the minimum required pieces  
   document store, retrieval step, prompt template, answer generation, scoring.

### Result  

Ended the day with a clear target  
one focused RAG flow instead of a vague idea of many possible projects.

---

## Day 2: Building the First RAG Prototype  

### Overview  

Moved from planning to an actual working path from question to answer.

### Work Done  

1. Loaded a small collection of reference text into a simple store that can be searched by chunks.  
2. Implemented a basic retrieval step that returns the top relevant chunks for a given query.  
3. Wired a first prompt template that takes system message, retrieved context and user question into a single request.  
4. Verified end to end behaviour with a few manual questions to confirm that the wiring is correct.

### Result  

We now have a minimal RAG prototype that can answer questions using retrieved context instead of hallucinating freely.

---

## Day 3: Applying the Evaluation Rubric  

### Overview  

The goal for this day was to stop trusting gut instinct and actually score answers using the rubric written last week.

### Work Done  

1. Collected around twenty real or realistic questions for the chosen use case.  
2. Ran them through the RAG prototype and captured the answers.  
3. Scored each answer with the rubric along several dimensions  
   relevance, grounding in context, clarity, and usefulness.  
4. Marked the cases where the rubric felt wrong or too forgiving.

### Result  

Now have a concrete set of question answer pairs with scores, and a first look at where the rubric is weak or misaligned with expectations.

---

## Day 4: Prompt Design and Iteration  

### Overview  

Focused on improving the answers by changing the prompts rather than touching the model.

### Work Done  

1. Reviewed the low scoring answers from Day 3 and grouped the failure modes  
   vague answers, missing details from context, or extra speculation.  
2. Adjusted the system prompt to be stricter about quoting only from retrieved context and admitting uncertainty.  
3. Tweaked the user facing instructions to request structured output where helpful, for example short summary plus direct steps.  
4. Re ran the same questions and rescored them to see if the changes actually improved the ratings.

### Result  

Several weak answers improved in both grounding and usefulness.  
Also saw clearly that prompt changes have limits when retrieval itself is poor, which prevents magical thinking about prompting.

---

## Day 5: Logging for RAG Requests and Responses  

### Overview  

Stopped guessing about behaviour and started capturing detailed logs.

### Work Done  

1. Added simple logging for each run  
   question, retrieved chunks, final answer and rubric scores.  
2. Saved logs in a structured format so they can be filtered by score, query type or document source.  
3. Reviewed a handful of very low scoring and very high scoring examples directly from the logs.  
4. Noted patterns where retrieval returned irrelevant chunks or where the model ignored important context.

### Result  

There's now a traceable record for each answer instead of a blurry memory.  
This makes future debugging and iteration much easier.

---

## Day 6: LLM Handbook Update  

### Overview  

Turned the week into documentation instead of letting it evaporate.

### Work Done  

1. Added a new chapter in the LLM handbook that describes  
   the RAG prototype, the prompt templates and the logging strategy.  
2. Documented common failure cases observed  
   weak retrieval, overloaded prompts and unclear instructions.  
3. Updated the evaluation rubric section with real examples where the rubric worked and where it failed.  
4. Wrote short checklists for future LLM experiments  
   define use case, set success metrics, wire logging, run and score.

### Result  

The LLM handbook is now more than notes from articles.  
It reflects our own experiments and gives us a repeatable process for the next prototype.

---

## Day 7: Review and Next Steps  

### Overview  

Ended the week by reviewing what actually changed and where to push next.

### Work Done  

1. Summarised the impact of the RAG prototype  
   it works for some cases, fails for others, and we know why.  
2. Reviewed average scores by dimension to see where the system is weakest.  
3. Listed three concrete improvement paths  
   better retrieval, richer context selection and minor prompt refinements.  
4. Noted ideas for a second very small prototype in a different domain to test how portable our process is.

### Result  

We now have a working RAG flow, an evaluation loop and a logging habit.  
The next step is not more theory, it is more experiments using the same disciplined pattern.
