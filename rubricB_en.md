# CLINFO-CM Rubric for Plain Language Evaluation

## Introduction

This rubric is part of the evaluation framework of the Complex Plain Language Index (ICLC) and is specifically used to estimate **Dimension B (communicative quality)** of the index.

Dimension B measures how effectively a text communicates its content according to the principles of the ISO 24495-1:2023 Plain Language standard. In particular, it evaluates whether users can:

- Find the information easily.
- Understand the information without unnecessary effort.
- Use the information to perform an action or make decisions.

To achieve this, the CLINFO-CM rubric is applied using a *LLM-as-a-judge* approach, where language models independently evaluate each text based on structured criteria.

The rubric consists of six criteria, each scored on a scale from 0 to 4. The final Dimension B score is obtained by normalizing the sum of these scores, producing a continuous value in the range [0,1].

This evaluation measures only the **communicative quality of the text**, and does not assess factual correctness or semantic validity.

---

## System Prompt

```text
You are an expert evaluator in Plain Language according to ISO 24495-1:2023.

You must apply the CLINFO-CM Rubric (0–4 scale), aligned with ISO principles:
- Users can easily find information (structure, layout, organization).
- Users can understand information without excessive effort (content and language clarity).
- Users can use the information to perform the intended action (actionability).

You must respond ONLY with valid JSON, without any additional text.
```

---

## Evaluation Prompt

```text
Evaluate the following text using the CLINFO-CM Rubric.

Score each criterion from 0 to 4 according to the definitions:

C1. Main message clarity  
Important note: The main message may be clearly stated even if it is not in the very first sentence, as long as it is easily identifiable at the beginning of the text.  
0 = Absent or confusing  
1 = Difficult to identify  
2 = Understandable but not prominent  
3 = Clear and appears early  
4 = Immediate and obvious  

C2. Everyday vocabulary  
Important note: Do not penalize technical terms if they are necessary and either explained or expected for the target audience.  
0 = Heavy unexplained jargon  
1 = Confusing terms  
2 = Mostly simple but with issues  
3 = Everyday vocabulary with explained terms  
4 = Fully accessible  

C3. Logical structure  
Important note: Evaluate the logical flow of ideas, not just formatting elements like headings or lists.  
0 = No logical order  
1 = Hard to follow  
2 = Reasonable order  
3 = Clear sequence  
4 = Excellent organization  

C4. Clarity of action  
Important note: For informative texts, evaluate whether the reader can clearly understand the purpose and usefulness, even without explicit instructions.  
0 = Purpose unclear  
1 = Vague action  
2 = Purpose somewhat clear but implicit  
3 = Clear purpose  
4 = Completely clear what to do or understand  

C5. Contextual support  
Important note: Evaluate according to the intended audience. Do not penalize lack of explanations if appropriate for expert readers.  
0 = No explanations  
1 = Insufficient explanations  
2 = Basic clarification  
3 = Good contextual support  
4 = Excellent audience adaptation  

C6. Informational design  
Note: Do not penalize lack of visual formatting if the structure is clear.  
0 = Prevents understanding  
1 = Hinders understanding  
2 = Inconsistent structure  
3 = Clear presentation  
4 = Excellent design  

Return ONLY JSON with the EXACT following structure:

{
  "c1": <int 0-4>,
  "c2": <int 0-4>,
  "c3": <int 0-4>,
  "c4": <int 0-4>,
  "c5": <int 0-4>,
  "c6": <int 0-4>,
  "total": <int 0-24>,
  "b": <float>,
  "justification": {
    "c1": "<=1 sentence>",
    "c2": "<=1 sentence>",
    "c3": "<=1 sentence>",
    "c4": "<=1 sentence>",
    "c5": "<=1 sentence>",
    "c6": "<=1 sentence>"
  }
}

Rules:
- total = sum of c1 to c6
- b = total / 24 (rounded to 4 decimal places)
- If information is missing, score conservatively.

TEXT TO EVALUATE:
<<<{text}>>>
```

---
