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


### transformers

- https://www.lesswrong.com/posts/CJsxd8ofLjGFxkmAP/explaining-the-transformer-circuits-framework-by-example
- https://medium.com/@sjonany/transformers-doing-math-e544b8486ff2
- https://towardsdatascience.com/transformers-and-attention-are-just-fancy-addition-machines/
- https://colab.research.google.com/drive/1F6_1_cWXE5M7WocUcpQWp3v8z4b1jL20#scrollTo=QoMukpTOzU-5
- 2402.02619
- 2405.17399
- 2310.13121
- https://www.alignmentforum.org/posts/btasQF7wiCYPsr5qw/200-cop-in-mi-techniques-tooling-and-automation
- https://www.alignmentforum.org/posts/o6ptPu7arZrqRCxyz/200-cop-in-mi-exploring-polysemanticity-and-superposition

@Olah2020


Interpreting and reverse engineering neural networks and transformers to find meaningful circuits
has been an area of active research. Olah et al. (2020a) argued that by studying the connections
between neurons and their weights, we can find meaningful algorithms (aka Circuits) in a “vision”
neural network. Elhage et al. (2021) extended this approach to transformers, conceptualizing their
operation in a mathematical framework that allows significant understanding of how transformer
operate internally. Various tools (Foote et al., 2023; Conmy et al., 2023b; Garde et al., 2023) use
this framework to semi-automate some aspects of reverse engineering. Nanda et al. (2023) reverse-
engineered modular addition (e.g. 5 + 7 mod 10 = 2) showing the model used discrete Fourier
transforms and trigonometric identities to convert modular addition to rotation about a circle.


# AI generated notes

## 2310.13121
Bereska’s taxonomy splits mechanistic interpretability into observational tools (e.g., attention and representation inspections) versus interventional techniques that perturb components to test causal roles, organized by causal nature, phase, locality, and comprehensiveness (papers/Bereska2024.txt:723, papers/Bereska2024.txt:731, papers/Bereska2024.txt:749). In 2310.13121 the authors visualize which tokens each attention head attends to and use those patterns to explain staging of the addition algorithm, placing their attention-mapping squarely in Bereska’s observational bucket (papers/2310.13121v9.txt:253, papers/2310.13121v9.txt:607).

Bereska highlights “developmental interpretability” for studying training dynamics and phase transitions as part of the MI toolkit (papers/Bereska2024.txt:1229, papers/Bereska2024.txt:1231). 2310.13121 leans on this method by tracking per-digit training loss curves, identifying distinct learning phases and independent refinement of digit circuits, which matches the developmental lens Bereska describes (papers/2310.13121v9.txt:198, papers/2310.13121v9.txt:606).

Among interventional methods, Bereska groups activation patching variants—explicitly including zero and mean ablations—as core causal tools (papers/Bereska2024.txt:723, papers/Bereska2024.txt:1077). The addition paper repeatedly performs mean and zero ablations on the residual stream and individual heads via TransformerLens to validate which components implement each subtask, directly instantiating this activation-patching family (papers/2310.13121v9.txt:486, papers/2310.13121v9.txt:550, papers/2310.13121v9.txt:1177).

Bereska emphasizes iterating between observation and intervention to build full circuit explanations (papers/Bereska2024.txt:1148). 2310.13121 follows that playbook: attention observations guide where to ablate, and the resulting causal tests confirm the algorithmic roles within the circuit description (papers/2310.13121v9.txt:606, papers/2310.13121v9.txt:608).

No evidence in 2310.13121 of other Bereska-listed methods like sparse autoencoders, structured probes, logit/tuned lens, causal scrubbing, or intrinsic approaches; the paper relies on the observational-attention plus activation-ablation toolkit combined with training-dynamics analysis. Possible next steps: 1) repeat the study with additional interventional tools such as path patching or causal abstraction to test robustness; 2) add observational cross-checks like the logit/tuned lens to verify predictions at intermediary layers.


Every technique in 2310.13121 lines up with categories Bereska already surveys. The paper combines observational attention-pattern inspection and training-dynamics analysis (papers/2310.13121v9.txt:198, papers/2310.13121v9.txt:253) with interventional ablations/patching (papers/2310.13121v9.txt:486, papers/2310.13121v9.txt:1177). All of those sit squarely inside Bereska’s observational, developmental, and activation-patching toolkits (papers/Bereska2024.txt:723, papers/Bereska2024.txt:1077, papers/Bereska2024.txt:1229). Even the “behavior filtering” step they mention for automated node search (papers/2310.13121v9.txt:1298, papers/2310.13121v9.txt:1379) is just a concrete instance of the automated circuit-discovery approaches Bereska highlights in the same taxonomy (papers/Bereska2024.txt:914, papers/Bereska2024.txt:1350). Nothing in 2310.13121 falls outside that coverage.