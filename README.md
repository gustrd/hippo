<p align="center" width="100%">
<img src="assets/hippo.png" alt="HIPPO" style="width: 20%; min-width: 300px; display: block; margin: auto;">
</p>

# HIPPO (High-level Interlingual Performance Proximity Optimized)

HIPPO is an automated benchmarking tool designed especially for language-optimized Large Language Models (LLMs). Our primary goal is to evaluate the efficacy of LLMs in terms of both grammatical accuracy and semantic closeness of translations. This dual assessment approach ensures that the translations are not only grammatically correct but also preserve the intended meaning of the original text.

The Jupyter Notebook that can be used to reproduce these calculations can be found [here](https://github.com/gustrd/hippo/blob/main/notebooks/hippo_benchmark_colab.ipynb). Or test it directly at Google Colab [here](https://colab.research.google.com/drive/1lvfepa5fwTkap6oYb7IlJkUqn4yR4FHB?usp=sharing)

# Features

- Automated Evaluation: No manual input required for routine evaluations.
- Dual Metrics: Ensures comprehensive assessment by focusing on grammatical accuracy as well as semantic proximity.
- Adaptable: Can be tailored to work with various LLMs that are specifically optimized for different languages.

# Structure

The benchmark is structured around two main phases: grammatical assessment and semantic assessment.

1. Grammatical Assessment:

- This phase evaluates the grammatical accuracy of translations.
- Utilizes the Grammatical Checker Tool for evaluation.
- A translation is deemed successful in this phase if no grammatical error is detected in its content.

2. Semantic Assessment:

- This phase assesses the semantic proximity between the model's translation and a reference translation.
- The Semantic Proximity Model is employed to determine the distance between the embeddings of the reference translation (sourced from the original dataset) and the translation generated by the model.
- A translation is deemed successful in this phase if the distance between the embeddings is less than the specified threshold parameter.

The benchmark's final score is an aggregate, taking into account only those sentences that successfully pass both the grammatical and semantic assessments.

# Current Configuration

- Corpus: [Opus100 validation subset](https://huggingface.co/datasets/opus100/viewer/en-pt/validation).
- Grammatical Checker Tool: [LanguageTool](https://github.com/languagetool-org/languagetool).
- Semantic Proximity Model: [all-MiniKM-L6-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2).

- Semantic parameters:
Threshold - 0.25

- Generation parameters:
Temperature: 0.3;
Top-P Value: 0.9;
Quantization : 4 bits (where applicable);

# Current Results

The table below presents the models we've evaluated for the [Cabra](https://github.com/gustrd/cabra) project, specifically focusing on translation from English to Portuguese.

| Model | Fine-tuned? | Original Model | Allows Commercial Use? |HIPPO-Opus100-Grammar | HIPPO-Opus100-Paraphrase | HIPPO-Opus100-Combined |
|-------|-------------|----------------|------------------------|----------------------|--------------------------|------------------------|
| Llama-7B | No | N/A | No | 6.11% | 8.91% | 2.10% |
| Canarim-7B | Yes | Falcon-7b | No | 22.85% | 21.45% | 6.50% |
| XGen-OpenInstruct-7B | Yes | XGen-7B | Yes | 32.20% | 29.90% | 8.50% |
| OpenLlama-Instruct-13B | Yes | OpenLlama-13B | Yes | 26.35% | 32.50% | 8.75% |
| OpenLlama-Alpaca3B-Cleaned | Yes | OpenLlama-3B | No | 30.35% | 30.90% | 10.00% |
| Cabrita-7B | Yes | Llama-7B | No | 34.00% | 33.85% | 10.60% |
| MPT-7B-Instruct | Yes | MPT-7B | Yes | 29.60% | 41.80% | 11.85% |
| Cabra-13B | Yes | OpenLlama-Instruct-13B | Yes | 35.75% | 37.75% | 12.40% |
| Alpaca-7B | Yes | Llama-7B | No | 32.60% | 46.30% | 15.25% |
| Zephyr-7B-Beta | Yes | Mistral-7B | Yes | 38.55% | 49.25% | 17.65% |
| GPT-3.5 | Yes | - | Yes (paid service) | 38.35% | 61.45% | 22.80% | 
| Maritaca | Yes | ? | ? | 40.80% | 59.50% | 23.15% | 
| GPT-4 | Yes | - | Yes (paid service) | 40.65% | 61.85% | 23.95% | 
| Google Translate (reference) | Not-LLM | Not-LLM | Yes | 39.85% | 64.30% | 24.45% |
| MarianMT (reference) | Not-LLM | Not-LLM | Yes | 41.65% | 69.35% | 26.80% |
| LibreTranslate (reference) | Not-LLM | Not-LLM | Yes | 44.55% | 66.40% | 27.90% |

# Preliminary Conclusions

- Repeatability: In our tests so far, we have observed a maximum variation of 1% in the scores across different generations. This is likely due to non-deterministic translation. Further testing with more examples is required to determine if this holds true for all models.

- Importance of Fine-tuning: There's evident merit in refining models as showcased by derivatives such as Alpaca-7B and Cabrita-7B, which originated from Llama-7B. These fine-tuned versions manifested superior performance, underscoring the value of task-specific fine-tuning or leveraging specialized datasets.

- Reference Models: The reference models, MarianMT for paraphrasing and LibreTranslate for grammar, consistently outperform other contenders in their specialized domains. MarianMT achieves prominence with the highest paraphrase success rate and average paraphrase chance. On the other hand, LibreTranslate stands out in ensuring grammatical accuracy. This pattern underscores the notion that while large language models (LLMs) have made substantial advancements, there remains a niche where specialized models excel.

- Performance Ceiling: There's a discernible limit to how well the current models perform. No model has yet achieved flawless output, with the pinnacle of grammatical accuracy resting below 45% and paraphrasing success not exceeding 70%. This observation points to a substantial scope for progression and optimization in the realms of translation and paraphrasing.

# Next Steps

- Benchmark Consistency: Enhance the repeatability and reliability of the benchmark results.

- Generation Methodology: Explore the merits and demerits of deterministic versus non-deterministic translation.

- Reference Enhancement: Seek and test superior reference benchmarks to enhance the assessment's accuracy and relevance.

- Grammatical Precision: Experiment with advanced grammatical error detection tools to elevate the accuracy of evaluations.

- Semantic Proximity Models: Probe into more sophisticated models for gauging semantic closeness, with a particular emphasis on multi-language capabilities.

# Contributing

We're open to contributions! If you've got suggestions, improvements, or find any bugs, please open an issue or submit a pull request.

