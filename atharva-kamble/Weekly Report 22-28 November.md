# Weekly Report: LLM Handbook Polishing and Support Prompt Experiments

**Date**: 22 to 28 November  
**Topics Covered**:  
LLM Handbook Structure Cleanup  
BimRide Support Use Case Selection  
Prompt Design and Manual Evaluation  

## Overview

This week I slowed the pace on new theory and focused on making what I already learned actually usable.  
I cleaned up the LLM handbook so it reads like a reference and not a raw notebook, chose one realistic BimRide support use case, and wrote and tested prompts for that scenario.  
The goal was to turn scattered notes into a tool I can lean on when I build or debug support flows later.

## Day 1: LLM Handbook Structure Cleanup

### Overview
Started by fixing the structure of the handbook so it is not a wall of text.

### Work Done
Split the handbook into clear sections for tokens, context windows, system prompts, retrieval, evaluation and examples.  
Moved duplicate content into a single place instead of repeating the same ideas in different sections.  
Added a simple table of contents at the top so I can jump to any topic quickly.

### Result
The handbook now feels like something I can open and navigate in a few seconds instead of hunting through random notes.

## Day 2: Removing Repetition and Tightening Explanations

### Overview
Focused on cutting noise and sharpening the explanations that were vague or repetitive.

### Work Done
Removed sentences that said the same thing three times without adding clarity.  
Rewrote fuzzy explanations around context windows and truncation into short and direct paragraphs.  
Highlighted key rules in each section so the main ideas stand out on a quick skim.

### Result
The handbook reads cleaner and I can see the core principles without getting lost in filler.

## Day 3: Adding Concrete Examples for Core Concepts

### Overview
Turned abstract concepts into concrete examples that I can reuse in future projects.

### Work Done
Added small examples for tokenization that show how a short sentence becomes tokens and why wording choices change token cost.  
Wrote examples that show how a long prompt can overflow a context window and what a safe prompt looks like instead.  
Added a simple before and after example of a weak system prompt versus a strong one for a help desk scenario.

### Result
I now have copy paste friendly examples that make each concept real instead of only theory.

## Day 4: Choosing and Scoping a BimRide Support Use Case

### Overview
Shifted from handbook cleanup to a real support scenario for BimRide.

### Work Done
Picked one concrete use case which is answering common rider questions about trip receipts, cancellations and refund status.  
Defined what this support flow should and should not do so it stays small enough to test.  
Listed ten sample questions that real riders might ask around receipts and refunds.

### Result
I have one focused support use case with a clear boundary instead of a vague idea of support automation.

## Day 5: Writing First Set of Prompts for the Use Case

### Overview
Designed prompts that could power this support scenario using the concepts from the handbook.

### Work Done
Wrote a system prompt that defines the role, tone and limits of the support agent for BimRide.  
Created three user prompt templates for receipt requests, cancellation questions and refund status checks.  
Embedded simple safety instructions and formatting rules in the system prompt so answers stay grounded and structured.

### Result
There is now a small set of concrete prompts tied to a real BimRide support task instead of only generic examples.

## Day 6: Manual Testing of Prompts on Sample Questions

### Overview
Put the prompts to work on a small test set to see how they behave in practice.

### Work Done
Ran the three prompt templates against the ten sample rider questions I wrote earlier.  
Logged when the model answered correctly, when it hallucinated missing data, and when the wording was unclear or too polite to be useful.  
Noted which system prompt instructions actually changed behaviour and which lines were ignored.

### Result
I now have a realistic view of how the prompts perform and where they break under simple stress.

## Day 7: Feeding Results Back Into the LLM Handbook

### Overview
Closed the loop by pushing lessons from the support experiment back into the handbook.

### Work Done
Added a short case study that walks through the BimRide support use case from problem to prompt to result.  
Updated the system prompt section with specific do and do not patterns that worked better in testing.  
Wrote a short checklist for future experiments which includes defining scope, writing system prompt, designing templates, testing on real questions, logging behaviour and refining.

### Result
The handbook is no longer just theory.  
It now includes one full real example and a small process I can reuse for future LLM work.
