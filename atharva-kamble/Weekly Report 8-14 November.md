# Weekly Report: LLM Fundamentals and Handbook Creation  
**Date:** 8 to 14 November  
**Topics Covered:**  
1. Tokenization and how prompts become tokens  
2. Context windows and prompt sizing  
3. System prompts for support and analytics  
4. Retrieval and RAG flow  
5. LLM evaluation and scoring rubrics  
6. Creation of a living LLM handbook  

---

## Overview  

This week was a focused sprint on understanding how large language models actually work in practice, not at buzzword level.  

The work was split into three layers  

* Core mechanics  
  * tokenization  
  * context limits  
* Control surface  
  * system prompts  
  * retrieval and RAG  
* Quality control  
  * evaluation  
  * a single handbook that ties everything into one place  

By the end of the week there is a clear internal reference for future work with LLMs so that any new experiment for BimRide or other projects starts from a solid base instead of guesswork.

---

## Day 1: Tokenization and Prompt Structure  

### Overview  

Focused on building a concrete mental model of how text is converted into tokens and why token count matters in every decision.

### Work Done  

1. Wrote a short internal note in plain language that answered three questions  
   * What exactly is a token  
   * How a sentence is split into tokens  
   * Why different models have different token limits  

2. Took several real prompts used in previous work  
   * weekly reports  
   * ride hailing descriptions  
   * support style questions  

   For each prompt  

   * counted the approximate tokens  
   * highlighted repeated phrases and unnecessary context  
   * rewrote a lean version that says the same thing with fewer tokens  

3. Added a section to the LLM handbook titled **Tokenization Basics** that contains  
   * a simple definition of a token  
   * two side by side examples  
     * long bloated prompt  
     * optimized shorter prompt  
   * notes on how token limits cap both input and output  

### Result  

Token count is no longer an abstract number. There is now a concrete feel for how much text actually fits inside a realistic budget and how careless writing wastes capacity.

---

## Day 2: Context Windows and Prompt Sizing  

### Overview  

Moved from tokens to full context windows and how to design prompts that fit safely within those limits.

### Work Done  

1. Defined three common use cases  

   * weekly report generation  
   * internal analytics explanation  
   * customer support answer  

   For each case wrote  

   * what information is absolutely required  
   * what is optional  
   * what is pure noise that can be removed  

2. Designed a compact context template for each use case that includes  

   * a short system instruction  
   * minimal but precise background  
   * the actual question or task  

3. Added a **Context Windows** section in the LLM handbook with  

   * a simple explanation of context limits  
   * examples of oversized prompts and their trimmed versions  
   * a checklist to review before sending any large prompt  

### Result  

Instead of throwing the entire history at the model, there is now a clear habit of asking what the model truly needs and designing prompts that respect the context budget.

---

## Day 3: System Prompts for Support and Analytics  

### Overview  

The focus shifted to system prompts and how to control behaviour across support and analytics scenarios.

### Work Done  

1. Drafted system prompts for three concrete cases  

   * customer support assistant for ride issues  
   * internal analytics explainer for dashboards and metrics  
   * technical assistant for weekly engineering reports  

2. For each case wrote  

   * an intentionally weak version of the system prompt  
   * an improved version with  

     * clear role definition  
     * constraints  
     * style guidelines  
     * forbidden behaviour  

   Then annotated exactly what changed between the two versions and why the improved one is safer and more useful.

3. Added a **System Prompt Patterns** section in the handbook containing  

   * the three final system prompts  
   * a short set of rules for good prompts  
     * be explicit about role and audience  
     * define what not to do  
     * state how to handle uncertainty  

### Result  

There are now reusable system prompts ready for real products and a pattern for how to design more without trial and error every time.

---

## Day 4: Retrieval and RAG Flow  

### Overview  

Shifted into retrieval augmented generation and how external data interacts with the model.

### Work Done  

1. Wrote a narrative explanation of the RAG flow in plain language  

   * user asks a question  
   * system converts it into an embedding  
   * similar documents are retrieved from a store  
   * the model sees both the question and the retrieved snippets  
   * the model generates an answer grounded in that context  

2. Picked one realistic use case  

   * support answering from internal documentation and previous weekly reports  

   For this case sketched  

   * how to chunk documents  
   * what to store as embeddings  
   * how many chunks to retrieve per query  
   * how to format the context passed to the model  

3. Created a simple diagram for the handbook that shows  

   * inputs  
   * retrieval step  
   * model step  
   * output  

   and added a worked example with a BimRide style question and the exact data that would flow through the system.

### Result  

RAG is no longer a buzzword. There is a clear step by step picture of what happens between the user question and the final answer and how system design choices affect quality.

---

## Day 5: LLM Evaluation and Scoring Rubric  

### Overview  

Focused on moving evaluation away from vague feelings and into a structured scoring approach.

### Work Done  

1. Chose one concrete use case  

   * generation of weekly status reports  

2. Defined a simple rubric with four criteria  

   * correctness  
   * coverage of the important points  
   * clarity and structure  
   * style fit for the intended audience  

   Each criterion scored from one to five with short descriptions of what each score means.

3. Took three previous model outputs  

   * one strong  
   * one average  
   * one weak  

   Scored each answer using the rubric and wrote short comments explaining the score.  

4. Added a **Evaluation and Rubrics** section to the handbook with  

   * the full rubric table  
   * one complete scoring example  
   * guidance on how to adapt the rubric for other tasks such as support replies or analytics explanations  

### Result  

There is now a repeatable way to judge answers instead of hand waving about quality and that can later be used to compare models or prompt versions.

---

## Day 6: LLM Handbook Consolidation  

### Overview  

Pulled together all the pieces into one living document and removed noise.

### Work Done  

1. Merged all notes from previous days into a single structured handbook with sections  

   * Tokenization basics  
   * Context windows and prompt sizing  
   * System prompt patterns  
   * Retrieval and RAG flow  
   * Evaluation and rubrics  

2. Edited aggressively  

   * removed duplicate explanations  
   * cut generic theory that does not help with real work  
   * tightened examples so they are fast to read  

3. Wrote a one page cheat sheet at the start covering  

   * quick rules for writing prompts  
   * common mistakes to avoid  
   * a mini checklist to review before building any new LLM feature  

### Result  

Instead of scattered notes and chat logs there is one document that can be reused every time a new LLM related task comes up.

---

## Day 7: Review and Next Steps  

### Overview  

Closed the sprint by reviewing what was learned and deciding the next move.

### Work Done  

1. Read the entire handbook as if seeing it for the first time and marked  

   * sections that were still vague  
   * explanations that assumed too much prior knowledge  

   Then rewrote those parts to be sharper and more direct.

2. Wrote a short reflection covering  

   * what now feels solid  
     * tokenization basics  
     * context design  
     * system prompt design  
   * what still feels early  
     * evaluation at scale  
     * more advanced retrieval strategies  

3. Listed potential tracks for the next sprint  

   * build a tiny RAG prototype using the handbook patterns  
   * design evaluation flows that handle larger sample sizes  
   * explore simple agent style workflows using strong system prompts and tools  

### Result  

The week ends with a clear foundation instead of scattered intuition and a realistic view of where to go deeper next.
