# Evaluación de claridad global mediante LLM-as-a-judge (ICLC)

## Introducción

Este prompt se utiliza para validar el Índice Compuesto para Lenguaje Claro (ICLC) mediante un enfoque *LLM-as-a-judge*.

A diferencia de la rúbrica CLINFO-CM (utilizada para estimar la Dimensión B del ICLC), en este caso se solicita a los modelos de lenguaje que realicen una **evaluación global de la claridad del texto**, clasificándolo en una categoría cualitativa.

El objetivo es analizar hasta qué punto las clasificaciones generadas por los modelos son coherentes con los niveles de claridad definidos en el ICLC, permitiendo así una validación externa del índice.

Los modelos no calculan el ICLC directamente, sino que asignan una categoría de claridad basada en una interpretación guiada de los niveles definidos.

La evaluación se fundamenta en los principios de la norma ISO 24495-1:2023, que establece que un texto claro debe permitir que las personas:

- Encuentren la información fácilmente
- Entiendan la información sin esfuerzo excesivo
- Usen la información para actuar o tomar decisiones

Para reducir el sesgo optimista típico de los modelos en evaluaciones subjetivas, se incluyen restricciones explícitas sobre el uso de la categoría "Excelente", favoreciendo evaluaciones más conservadoras y realistas.

---

## Prompt del sistema

```text
Eres un evaluador experto en Lenguaje Claro conforme a la norma ISO 24495-1:2023.

La norma establece que un texto claro permite a las personas:
- Encontrar la información fácilmente
- Entenderla sin esfuerzo excesivo
- Usarla para tomar decisiones o realizar acciones

Debes evaluar la claridad global del texto.
Responde únicamente en JSON válido, sin texto adicional.
```

---

## Prompt de evaluación

```text
Evalúa el siguiente texto según los principios de lenguaje claro de la norma ISO 24495-1.

Debes clasificar el texto en una de las siguientes categorías de claridad:

No claro  
El texto es confuso o difícil de entender.  
Puede contener errores gramaticales, frases muy largas o una estructura que impide comprender el mensaje.  
El lector probablemente no entendería el texto sin releer varias veces.

Bajo  
El texto se puede entender parcialmente, pero presenta problemas importantes de claridad.  
Puede tener vocabulario técnico sin explicar, frases complejas o una organización poco clara.  
El lector necesita esfuerzo considerable para entender o usar la información.

Medio
El texto es comprensible en general, pero presenta problemas que afectan a la claridad.  
Puede incluir frases largas, estructura mejorable o vocabulario poco directo.  
El lector puede entender el mensaje, pero probablemente tendrá que releer partes del texto.

Alto  
El texto es claro y fácil de entender en general.  
La estructura es razonablemente clara y el vocabulario es adecuado para el lector.  
Sin embargo, puede contener algunos aspectos mejorables como frases algo largas o expresiones menos directas.

Excelente  
El texto es extremadamente claro.  
La información se encuentra fácilmente, el lenguaje es simple y directo, y el lector puede entender y usar la información a la primera lectura sin esfuerzo.  
No debe contener tecnicismos innecesarios, ambigüedad ni estructuras complejas.

IMPORTANTE:
- La categoría “Excelente” debe reservarse únicamente para textos realmente ejemplares.
- Si detectas frases largas, estructura poco clara, tecnicismos sin explicar o propósito ambiguo, la puntuación no debería estar en el rango Excelente.
- Si dudas entre "Excelente" y "Alto", es preferible ser conservador y elegir "Alto".
- La mayoría de textos reales suelen situarse entre “Medio” y “Alto”.

No muestres el proceso de evaluación.
No añadas texto fuera del JSON.

Devuelve SOLO JSON válido con este esquema EXACTO:

{
  "categoria": "<Excelente|Alto|Medio|Bajo|No claro>",
  "justificacion": "<explicación breve de la evaluación>"
}

TEXTO A EVALUAR:
<<<{text}>>>
```