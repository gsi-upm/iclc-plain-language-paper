# Global clarity evaluation using LLM-as-a-judge (ICLC)

## Introduction

This prompt is used to validate the Complex Plain Language Index (ICLC) using a *LLM-as-a-judge* approach.

Unlike the CLINFO-CM rubric (used to estimate Dimension B of the ICLC), this prompt asks language models to perform a **global assessment of text clarity**, assigning each text to a qualitative category.

The goal is to analyze whether model-generated classifications are consistent with the clarity levels defined in the ICLC framework, thereby providing an external validation of the index.

Models do not compute the ICLC directly. Instead, they classify texts based on an interpretation of clarity levels defined.

The evaluation is grounded in the ISO 24495-1:2023 standard, which states that a clear text should enable users to:

- Find information easily  
- Understand it without unnecessary effort  
- Use it to take action or make decisions  

To mitigate the well-known optimistic bias of language models in subjective evaluations, explicit constraints are introduced to limit the use of the "Excellent" category, encouraging more conservative and reliable judgments.

---

## System Prompt

```text
You are an expert evaluator in Plain Language according to ISO 24495-1:2023.

The standard states that a clear text allows users to:
- Find information easily
- Understand it without excessive effort
- Use it to make decisions or perform actions

You must evaluate the overall clarity of the text.
Respond only with valid JSON, without additional text.
```

---

## Evaluation Prompt

```text
Evaluate the following text according to the principles of plain language from ISO 24495-1.

You must classify the text into one of the following clarity categories:

Not clear  
The text is confusing or difficult to understand.  
It may contain grammatical issues, very long sentences, or a structure that prevents understanding.  
The reader would likely need to reread multiple times.

Low  
The text is partially understandable but presents significant clarity issues.  
It may include unexplained technical vocabulary, complex sentences, or unclear organization.  
The reader needs considerable effort to understand or use the information.

Medium
The text is generally understandable but includes issues that affect clarity.  
It may contain long sentences, suboptimal structure, or indirect vocabulary.  
The reader can understand the message but may need to reread parts.

High  
The text is generally clear and easy to understand.  
The structure is reasonably clear and the vocabulary is appropriate.  
However, some improvements are still possible like slightly long sentences or less direct phrasing.

Excellent  
The text is extremely clear.  
Information is easy to find, language is simple and direct, and the reader can understand and use the content on the first reading without effort.  
It should not contain unnecessary technical terms, ambiguity, or complex structures.

IMPORTANT:
- The “Excellent” category must be reserved only for truly exemplary texts.
- If you detect long sentences, unclear structure, unexplained jargon, or ambiguous purpose, the text should not be rated as Excellent.
- If unsure between "Excellent" and "High", choose "High" to maintain category integrity.
- Most real-world texts fall between “Medium” and “High”.

Do not show your reasoning process.
Do not add any text outside the JSON.

Return ONLY valid JSON with the EXACT following structure:

{
  "category": "<Excellent|High|Medium|Low|Not clear>",
  "justification": "<brief explanation>"
}

TEXT TO EVALUATE:
<<<{text}>>>
```

---