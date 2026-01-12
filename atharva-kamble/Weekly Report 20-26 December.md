# Weekly Report: Codex Model Testing Playground
**Date:** December 20 to December 26

## Focus Areas
* Setting up a minimal testing environment for prompt experimentation
* Designing a narrow, repeatable task for model comparison
* Testing across multiple OpenAI models without optimization
* Capturing raw observations on behavior and consistency
* Documenting the process and findings in the handbook

## Overview
This week focused on establishing a small, controlled playground for testing Codex-style prompts against OpenAI models. The work remained deliberately narrow: one simple task, one fixed prompt, and a handful of test cases run across two models. No optimization was attempted. The goal was to observe differences in behavior, consistency, and instruction following, then document everything cleanly for future reference.

---

## Day 1: Defining the Test Task and Scope
**Overview:** Selected a narrow support ticket transformation task as the testing foundation.

**Work Done:**
* Chose "extract structured fields from a support ticket" as the test task
* Defined required output fields: category, priority, sentiment, action needed
* Created three sample support tickets with varying clarity and tone
* Documented the expected output structure before writing any prompts

**Result:** A clear, repeatable task was established that could expose differences in model behavior without unnecessary complexity.

---

## Day 2: Building the Testing Playground
**Overview:** Set up a minimal environment to run prompts and capture outputs systematically.

**Work Done:**
* Created a simple script to send prompts to OpenAI's API
* Built a structure to store prompt, input, model name, and raw output together
* Verified the script worked with a basic test call
* Avoided adding features beyond what was needed to run and record tests

**Result:** A working playground existed that could execute the same prompt and inputs across different models with minimal friction.

---

## Day 3: Writing the Initial Codex-Style Prompt
**Overview:** Designed a simple, directive prompt for the support ticket transformation task.

**Work Done:**
* Wrote a system prompt that specified the task, output format, and field definitions
* Kept instructions minimal and direct without excessive guidance
* Avoided pre-optimizing for edge cases or ambiguity
* Saved the prompt as a fixed baseline for all tests

**Result:** A clear, unoptimized Codex-style prompt was ready to test without assumptions about what would work best.

---

## Day 4: First Model Testing - GPT-3.5-turbo
**Overview:** Ran the prompt and test inputs through GPT-3.5-turbo to establish a baseline.

**Work Done:**
* Executed all three test cases using the fixed prompt
* Captured raw outputs exactly as returned by the model
* Noted initial observations on field extraction accuracy and format adherence
* Recorded response time for each test case

**Result:** A complete set of GPT-3.5-turbo outputs was documented, showing consistent formatting but occasional misclassification of priority.

---

## Day 5: Second Model Testing - GPT-4
**Overview:** Ran the same prompt and inputs through GPT-4 to compare behavior.

**Work Done:**
* Executed the identical test cases using GPT-4 with no prompt changes
* Captured outputs in the same format for direct comparison
* Noted differences in field accuracy, especially for sentiment and category
* Recorded noticeably longer response times compared to GPT-3.5-turbo

**Result:** GPT-4 outputs showed higher accuracy in ambiguous cases but with slower response times, revealing a clear tradeoff.

---

## Day 6: Observation Documentation and Comparison
**Overview:** Analyzed differences between models without attempting to explain or optimize.

**Work Done:**
* Compared outputs field by field across both models for each test case
* Documented where GPT-4 outperformed GPT-3.5-turbo and where behavior was similar
* Noted GPT-3.5-turbo's tendency toward generic categorization
* Captured observations on instruction following, format consistency, and edge case handling

**Result:** Clear behavioral differences were identified and recorded factually without premature conclusions or adjustments.

---

## Day 7: Handbook Documentation and Wrap-Up
**Overview:** Created a "Codex Testing Note" section in the handbook with the week's findings.

**Work Done:**
* Added a new section documenting the test task, prompt, and model configurations
* Included all three test inputs with side-by-side outputs from both models
* Summarized key observations on speed, consistency, and accuracy
* Noted areas for future exploration without committing to next steps

**Result:** The week ended with a documented, repeatable testing setup and a clean record of initial findings ready for future iterations.
