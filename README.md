# CLINFO-CM Evaluation Prompts and ICLC Validation

This repository contains the prompts used in the evaluation of plain language within the CLINFO framework and the validation of the Complex Plain Language Index (ICLC).

The prompts are designed to ensure reproducibility and transparency in the evaluation process, following the principles of the ISO 24495-1:2023 Plain Language standard.

---

## Overview

The evaluation framework is based on two complementary approaches:

1. **Rubric-based evaluation (Dimension B of ICLC)**  
2. **Global clarity classification (LLM-as-a-judge validation of ICLC)**  

These approaches serve different but related purposes in the assessment of text clarity.

---

## Files

### 1. CLINFO-CM Rubric (Dimension B)

- `rubricB_en.md` — English version  
- `rubricB_es.md` — Spanish version  

These prompts are used to evaluate the **communicative quality** of a text, corresponding to **Dimension B of the ICLC**.

They implement a rubric-based scoring system (0–4) across six criteria:

- Main message clarity  
- Everyday vocabulary  
- Logical structure  
- Clarity of action  
- Contextual support  
- Informational design  

The scores are aggregated and normalized to produce a continuous value in the range [0,1].

This evaluation follows a structured *LLM-as-a-judge* approach, where multiple language models independently assess each text.

---

### 2. Global Clarity Evaluation (ICLC Validation)

- `iclc_judge_eval_en.md` — English version  
- `iclc_judge_eval_es.md` — Spanish version  

These prompts are used to perform a **global classification of text clarity**, assigning each text to one of five categories:

- Not clear  
- Low  
- Medium
- High  
- Excellent  

This classification is used to **validate the ICLC**, by comparing model-generated clarity levels with the index values.

Unlike the rubric-based approach, models do not compute the ICLC directly. Instead, they classify texts based on an interpretation of clarity levels defined by the authors.

---

## Usage

Each markdown file contains:

- A methodological introduction  
- The system prompt  
- The evaluation prompt  

To reproduce the evaluation:

1. Load the system prompt  
2. Insert the target text into the evaluation template  
3. Execute the prompt using a language model  
4. Parse the JSON output  

---
