---
bibliography: ref.bib
---


# Survey



| Title                                                                                                      | Bibkey       | Category | TODO                        |
| ---------------------------------------------------------------------------------------------------------- | ------------ | -------- | --------------------------- |
| A Survey on Mechanistic Interpretability for Multi-Modal Foundation Models                                 | @Lin2025     | Survey   | [R](notes/lin2025survey.md) |
| Survey on the Role of Mechanistic Interpretability in Generative AI                                        | @Ranaldi2025 | Survey   |                             |
| Mechanistic Interpretability for AI Safety -- A Review                                                     | @Bereska2024 | Survey   |                             |
| Exploring Mechanistic Interpretability in Large Language Models: Challenges, Approaches, and Insights      | @Gantla2025  | Survey   |                             |
| A Mathematical Framework for Transformer Circuits                                                          | @Elhage2021  | Circuits | [R](notes/circuits.md)      |
| A Practical Review of Mechanistic Interpretability for Transformer-Based Language Models                   | @Rai2025     | Survey   |                             |
| A Survey on Neural Network Interpretability                                                                | @Zhang2021   | survey   |                             |
| Mechanistic interpretability of large language models with applications to the financial services industry | @Golgoon2024 | Survey   |                             |







### Intervention-Based Analytical Methods
To achieve mechanistic understanding, researchers have developed several key intervention-based methods that we will explore in this research:


- Correlational visualization computes and visualizes correlations between hidden states and final outputs, offering a macroscopic view of information flow within the model [@Vig2020]. 
- Causal tracing measures the effect of restoring early-layer representations on final output decisions, allowing for the identification of critical components influencing model behavior [@Meng2022;@Meng2022a;@Nanda2022]. 
- Representation similarity analysis quantifies the evolution of semantic concepts across layers using various similarity metrics, shedding light on how models process and refine information at different stages [@Kriegeskorte2008;@Nili2014].
- Circuit analysis combines observational and intervention approaches to map and test causal circuits of attention heads, neurons, and residual streams. This method first identifies potential circuits through pattern analysis, then validates these circuits through targeted interventions such as ablation studies and activation patching, providing a granular understanding of model computations [@Rai2024;@Olah2020;@Olah2022;@Elhage2021].

For Objectives 2 and 3, we will extend these methods to analyze prompt-behavior relationships and test model steering techniques:

- Identifying how specific prompt templates consistently alter activation patterns in specific layers and attention heads [@Wei2022].
- Testing whether injecting known "helpfulness" or "accuracy" representation directions can improve the reliability and factuality of model outputs in high-stakes crisis scenarios [@Turner2023;@Zou2023].