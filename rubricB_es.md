# Rúbrica CLINFO-CM para evaluación de Lenguaje Claro

## Introducción

Esta rúbrica forma parte del sistema de evaluación del Índice Compuesto de Lenguaje Claro (ICLC) y se utiliza específicamente para estimar la **Dimensión B (calidad comunicativa)** del índice.

La Dimensión B mide la calidad con la que un texto comunica su contenido conforme a los principios de la norma ISO 24495-1:2023 de Lenguaje Claro, es decir, si el texto permite que las personas:

- Encuentren la información con facilidad.
- Comprendan la información sin esfuerzo excesivo.
- Utilicen la información para realizar una acción o tomar decisiones.

Para ello, se emplea la rúbrica CLINFO-CM, que es aplicada por modelos de lenguaje (LLMs) en un esquema *LLM-as-a-judge*. Cada modelo evalúa el texto de forma independiente siguiendo criterios estructurados.

La rúbrica consta de seis criterios evaluados en una escala de 0 a 4. El valor final de la Dimensión B se obtiene normalizando la suma de las puntuaciones, produciendo un valor continuo en el rango [0,1].

Esta evaluación mide exclusivamente la **calidad comunicativa del texto**, y no su corrección factual ni su adecuación semántica.

---

## Prompt del sistema

```text
Eres un evaluador experto en Lenguaje Claro conforme a la norma ISO 24495-1:2023.

Debes aplicar la Rúbrica CLINFO-CM (escala 0–4) alineada con los principios ISO:
- Encuentren la información con facilidad (estructura, diseño, organización).
- Entender la información sin esfuerzo excesivo (claridad del contenido y del lenguaje).
- Poder usar la información para realizar la acción deseada (accionabilidad).

Debes responder únicamente en JSON válido, sin texto adicional.
```

---

## Prompt de evaluación

```text
Evalúa el siguiente texto con la Rúbrica CLINFO-CM.

Valora cada criterio entre 0 y 4 según las definiciones:

C1. Claridad del mensaje principal  
Nota importante: El mensaje principal puede estar claramente formulado aunque no aparezca en la primera frase exacta, siempre que sea identificable sin esfuerzo al inicio del texto.  
0 = No aparece o es confuso  
1 = Difícil de identificar  
2 = Comprensible pero no destacado  
3 = Claro y aparece al inicio  
4 = Inmediato y evidente  

C2. Vocabulario cotidiano  
Nota importante: No penalices términos técnicos si son necesarios y están explicados o son previsibles para el público objetivo.  
0 = Jerga abundante sin explicar  
1 = Términos confusos  
2 = Lenguaje simple con dificultades  
3 = Vocabulario cotidiano con términos explicados  
4 = Totalmente accesible  

C3. Estructura lógica  
Nota importante: Evalúa la lógica y progresión de ideas, no solo elementos visuales como títulos o listas.  
0 = Sin orden lógico  
1 = Difícil de seguir  
2 = Orden razonable  
3 = Secuencia clara  
4 = Excelente organización  

C4. Claridad de la acción  
Nota importante: Si el texto es informativo, evalúa si permite entender claramente su utilidad aunque no haya una acción explícita.  
0 = No se entiende para qué sirve  
1 = Acción vaga  
2 = Propósito comprensible pero poco explícito  
3 = Propósito claro  
4 = Totalmente claro qué hacer o entender  

C5. Apoyo contextual  
Nota importante: Evalúa según el público objetivo. No penalices si el texto es adecuado para expertos.  
0 = Sin explicaciones  
1 = Explicaciones insuficientes  
2 = Aclaraciones básicas  
3 = Buen apoyo contextual  
4 = Excelente adaptación al público  

C6. Diseño informativo  
Nota: No penalices ausencia de formato visual si el texto es claro estructuralmente.  
0 = Impide comprensión  
1 = Dificulta comprensión  
2 = Estructura inconsistente  
3 = Presentación clara  
4 = Diseño excelente  

Devuelve SOLO JSON con este esquema EXACTO:

{
  "c1": <int 0-4>,
  "c2": <int 0-4>,
  "c3": <int 0-4>,
  "c4": <int 0-4>,
  "c5": <int 0-4>,
  "c6": <int 0-4>,
  "total": <int 0-24>,
  "b": <float>,
  "justificacion": {
    "c1": "<=1 frase>",
    "c2": "<=1 frase>",
    "c3": "<=1 frase>",
    "c4": "<=1 frase>",
    "c5": "<=1 frase>",
    "c6": "<=1 frase>"
  }
}

Reglas:
- total = suma de c1 a c6
- b = total / 24 (redondeado a 4 decimales)
- Si falta información, puntúa de forma conservadora.

TEXTO A EVALUAR:
<<<{text}>>>
```

---