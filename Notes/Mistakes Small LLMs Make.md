---
tags:
- llm
---
## **Mistakes Small LLMs Make

The discussion above highlights several interesting points about the weaknesses and mistakes that small LLMs (Large Language Models) can make, especially in the context of numerical calculations and logical consistency. Let me summarize the key mistakes that are described:

### 1. **Inconsistent Calculation Results**

- Different instances of the same model (e.g., Llama 3.2 and Llama 3.2 3B) produce different results for the same calculations, which indicates inconsistency in the output.
- When adding or subtracting the same values, the results varied inexplicably between models, sometimes even when the inputs were identical.

### 2. **Hallucinations**

- These models often "hallucinate" values that aren't in line with the expected calculations. For instance, subtracting a value from itself should yield zero, but instead, the model produced non-zero values.
- There were cases where LLMs returned outputs like "0.7" or "-0.1" when those results should not have occurred based on arithmetic laws.

### 3. **Misleading Confidence Levels**

- The models frequently gave their confidence as "100%" even when the answers were incorrect. This misleading confidence is problematic as it suggests certainty where there shouldn't be any.
- Llama models gave conflicting probabilities of correctness, often stating very high (e.g., 99.99%) confidence even when they were clearly mistaken.

### 4. **Errors in Recalculations**

- When prompted to verify or re-calculate values, the models produced different results from previous attempts. This reflects difficulty in maintaining consistent logic through repeated calculations.
- In some cases, upon rechecking, the models provided new results like "0.9" or "0.7" without any proper reasoning as to why the previous calculations were incorrect.

### 5. **Failure in Complex Reasoning Tasks**

- When faced with a series of operations or more complex logic tasks (like analyzing values A, B, C, D), the models struggled to maintain accuracy.
- They had trouble dealing with multi-step problems, and their logical flow often broke down when multiple values were introduced or chained together.

### 6. **Overcomplicating Problems**

- Some LLMs added unnecessary steps or calculations that were not part of the original problem. This not only led to errors but also suggested that the models were unable to simplify or logically interpret basic tasks.
- Introducing additional operations, like adding a number instead of subtracting it, further complicated what should have been straightforward calculations.

### 7. **Disagreement Between Models**

- The same models, even when side by side, provided different results for identical tasks. This shows that small LLMs lack determinism in their outputs, meaning that you can't fully trust consistency across the same model type.
- While one model might correctly conclude a value like "0.9," another might end with a wrong value such as "0.4," even if both were given identical initial conditions.

### 8. **Unreliable Logical Reasoning and Verification**

- When attempting to verify logic or validate earlier steps, the models often contradicted themselves, which indicates they have limited capacity for multi-step reasoning.
- Despite running a "chain of reasoning" or "chain of sword," the output still contained incorrect values, meaning the verification process did not help rectify initial mistakes.

### 9. **Lack of Doubt or Self-Correction Mechanism**

- The models demonstrated an inability to doubt their results, which can be risky. They lacked the capacity for self-reflection to identify that their calculations could be flawed.
- The described recalculations often led to more confusion or changing answers without a concrete understanding of why the original answers were incorrect.

### Summary and Takeaway

The discussion demonstrates that small LLMs, like Llama 3.2 and other versions mentioned, are not reliable for complex arithmetic calculations, logical consistency, or tasks requiring step-by-step validation. These issues point to:

- **Numerical Instability**: Due to the inherent nature of language models and their architecture, performing arithmetic operations is not their strength. LLMs are designed for text understanding and generation, not precise numerical computation.
- **Lack of Logical Consistency**: They often struggle with problems that require consistent logical reasoning over several steps, leading to different results for the same problem.
- **False Confidence**: The high confidence levels despite errors make them particularly unreliable without human oversight, especially in critical domains like financial analysis or national security.

If you are using LLMs for tasks requiring precise numerical calculations or logical validation, it is important to keep these limitations in mind. For such use cases, traditional computation engines or rule-based systems may offer more reliability than relying solely on small LLMs.

[[LLM]]