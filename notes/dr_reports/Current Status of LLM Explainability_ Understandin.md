<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Current Status of LLM Explainability: Understanding What Each Layer Does

## Current Progress in LLM Interpretability

The field of mechanistic interpretability has made significant strides in 2024-2025, moving from purely descriptive analyses to **actionable insights that can be used to modify and improve model behavior**. Recent developments have improved our ability to trace model outputs back to both inputs and training data, with researchers now able to connect insights to actual model behavior rather than just describing internal states.[^1]

**Modern interpretability has evolved into practical, even real-time tools** that developers can integrate with just a few lines of code. The 2024-2025 period has transformed many interpretability techniques from research-only methods into production-ready tools, with visualization dashboards making it feasible to include interpretability directly in the model development loop.[^1]

## Understanding Layer Functions in Transformers

### General Layer Hierarchy

Research reveals that **transformer layers follow a hierarchical pattern of processing**:[^2][^3]

**Early Layers (1-4)**: Focus on low-level features including colors, patterns, basic syntactic elements, and edge detection. These layers show minimal task impact when ablated, with only slight increases in loss (approximately 0.11%).[^4][^3]

**Middle Layers (5-8)**: Process intermediate concepts and begin building more complex representations. In vision transformers, these layers transition from basic patterns to more meaningful visual concepts.[^3]

**Later Layers (9-12)**: Handle high-level semantic processing and task-specific computations. Deep attention heads in these layers cause significantly higher loss increases when removed (approximately 0.34%), demonstrating their critical importance for final predictions.[^4]

### Layer-Specific Functions by Domain

**Vision Transformers**: Follow a clear progression from colors to classes, with early layers focusing on colors and patterns, then gradually building complex concepts in later layers. During fine-tuning, the concepts change and the number of concepts reduces.[^3]

**Audio Transformers**: Show distinct specialization where early layers process speaker information, while middle layers handle content and word information.[^3]

**Language Models**: Demonstrate similar hierarchical processing, with **early layers handling basic linguistic features and later layers managing complex semantic relationships and reasoning**.[^5][^6]

## Modern Popular Interpretability Tools

### Core Libraries and Frameworks

**TransformerLens**: The most widely-used library for mechanistic interpretability, supporting 50+ open source language models. It allows researchers to cache any internal activation and edit, remove, or replace activations as the model runs. Originally created by Neel Nanda, it's designed specifically for GPT-2 style language models.[^7]

**Captum**: Facebook's comprehensive interpretability library for PyTorch models, supporting multi-modal interpretability across vision, text, and other domains. It includes state-of-the-art algorithms like Integrated Gradients, TCAV, and TracIn influence functions.[^8][^9]

**CircuitsVis**: Specialized for visualizing attention patterns and circuit analysis in transformers, commonly used alongside TransformerLens for mechanistic interpretability research.[^10][^11]

### Emerging Tools and Frameworks

**Sparse Autoencoders (SAEs)**: Have become the dominant method for decomposing neural network activations into interpretable features. SAEs with TopK activation enforce sparsity while maintaining reconstruction quality. Recent work shows approximately 80% of SAE features receive "yes" ratings for interpretability.[^12][^13]

**Prisma**: A new open-source framework designed specifically for vision mechanistic interpretability, providing unified toolkit access to 75+ vision and video transformers with support for SAE training.[^14]

**Inseq**: Focuses on interpretability for sequence generation models, particularly useful for understanding text generation processes.[^10]

### Specialized Analysis Tools

**Attention Analysis Tools**: Including BertViz for attention visualization, allowing researchers to examine how attention patterns develop across layers and heads.[^15][^10]

**Probing Methods**: Enable systematic investigation of what information is encoded at different layers, helping researchers understand the hierarchical organization of learned representations.[^5]

**Activation Patching**: Allows causal interventions to determine which components are necessary for specific behaviors, providing stronger evidence than purely correlational methods.[^5]

## Advanced Techniques for Layer Analysis

### Mechanistic Circuit Discovery

Recent work has moved toward **identifying computational circuits - subgraphs of model components with functional interpretations**. The ModCirc framework represents a breakthrough in discovering task-agnostic functional units that can be reused across different language tasks.[^16]

### Feature Attribution Methods

**Contrast-CAT**: A novel activation contrast-based attribution method that improves token-level attribution by filtering out class-irrelevant features from activations, showing significant improvements over existing methods.[^17]

**Layer-wise Relevance Propagation (LRP)**: Enables researchers to compute relevancy scores that propagate through attention layers and skip connections, maintaining total relevancy across layers.[^18]

### Automated Interpretation

**Automated Feature Explanation**: Uses large language models to automatically generate explanations for neuron behavior, scaling interpretation beyond manual analysis.[^10]

**Multi-exit Model Analysis**: Recent work shows that representation similarity increases between closer layers, enabling early exit strategies where models can make predictions from intermediate layers.[^6]

## Evaluation and Validation

Modern interpretability research emphasizes rigorous evaluation through multiple criteria:[^5]

**Faithfulness**: Whether explanations accurately reflect the model's actual decision-making process
**Completeness**: How much of the model's behavior the explanation accounts for
**Plausibility**: Whether explanations align with human intuitions about the task

## Future Directions and Challenges

The field is moving toward **automated hypothesis generation and standardized benchmarks**. Key challenges include scaling interpretability methods to larger models, developing better evaluation metrics, and creating more practical applications for model enhancement and AI safety.[^5]

**Integration with compliance and auditing processes** is becoming increasingly important as LLMs enter high-stakes domains like healthcare, finance, and law, where regulatory requirements demand transparency and accountability.[^1]

The mechanistic interpretability field has grown rapidly, with an estimated 50 full-time positions focused on this topic and increasing investment from major AI companies. This growth reflects both the practical importance of understanding these systems and the promising early results in making neural networks more interpretable and controllable.[^19]
<span style="display:none">[^20][^21][^22][^23][^24][^25][^26][^27][^28][^29][^30][^31][^32][^33][^34][^35][^36][^37][^38][^39][^40][^41][^42][^43][^44]</span>

<div style="text-align: center">⁂</div>

[^1]: https://www.rohan-paul.com/p/explainability-and-interpretability

[^2]: https://poloclub.github.io/transformer-explainer/

[^3]: https://www.youtube.com/watch?v=pSPuvpABKbM

[^4]: https://arxiv.org/pdf/2503.18762.pdf

[^5]: https://arxiv.org/html/2407.02646v1

[^6]: https://openreview.net/forum?id=vVxeFSR4fU

[^7]: https://github.com/TransformerLensOrg/TransformerLens

[^8]: https://captum.ai

[^9]: https://github.com/pytorch/captum

[^10]: https://github.com/JShollaj/awesome-llm-interpretability

[^11]: https://www.lesswrong.com/posts/oGEPwK6bvPNcEfD74/visualizing-interpretability

[^12]: https://www.pnas.org/doi/10.1073/pnas.2506316122

[^13]: https://pmc.ncbi.nlm.nih.gov/articles/PMC11839115/

[^14]: https://arxiv.org/html/2504.19475v1

[^15]: https://dev.to/nareshnishad/day-45-interpretability-techniques-for-llms-2m2c

[^16]: https://openreview.net/forum?id=do5vVfKEXZ

[^17]: https://openreview.net/forum?id=irCuIdCdAl

[^18]: https://openaccess.thecvf.com/content/CVPR2021/papers/Chefer_Transformer_Interpretability_Beyond_Attention_Visualization_CVPR_2021_paper.pdf

[^19]: https://transformer-circuits.pub/2024/april-update/index.html

[^20]: https://github.com/interpretingdl/eacl2024_transformer_interpretability_tutorial

[^21]: https://arxiv.org/abs/2507.08017

[^22]: https://arxiv.org/html/2504.00125v1

[^23]: https://www.turing.com/resources/top-llm-trends

[^24]: https://arxiv.org/abs/2407.11215

[^25]: https://hatchworks.com/blog/gen-ai/large-language-models-guide/

[^26]: https://openreview.net/pdf/2e54bc7a4d5a95f64c87a3b8290c25a2cbdaf729.pdf

[^27]: https://arxiv.org/html/2407.02646v2

[^28]: https://en.wikipedia.org/wiki/Transformer_(deep_learning_architecture)

[^29]: https://intuitionlabs.ai/articles/mechanistic-interpretability-ai-llms

[^30]: https://blog.mlq.ai/llm-transformer-architecture/

[^31]: https://aclanthology.org/2024.findings-acl.242.pdf

[^32]: https://captum.ai/tutorials/TorchVision_Interpret

[^33]: https://lakefs.io/blog/llm-observability-tools/

[^34]: https://www.reddit.com/r/MachineLearning/comments/1bxk9f7/d_good_booksresources_for_interpretability_in/

[^35]: https://github.com/ruizheliUOA/Awesome-Interpretability-in-Large-Language-Models

[^36]: https://seantrott.substack.com/p/mechanistic-interpretability-for

[^37]: https://www.reddit.com/r/MachineLearning/comments/lipl90/p_transformers_interpret_explainable_ai_for/

[^38]: https://www.lesswrong.com/posts/hnzHrdqn3nrjveayv/how-to-transformer-mechanistic-interpretability-in-50-lines

[^39]: https://openreview.net/forum?id=NB8qn8iIW9

[^40]: https://www.transformer-circuits.pub/2022/mech-interp-essay

[^41]: https://www.emergentmind.com/topics/layerflow

[^42]: https://arxiv.org/html/2505.16004v1

[^43]: https://www.neelnanda.io/mechanistic-interpretability/getting-started

[^44]: https://d2l.ai/chapter_attention-mechanisms-and-transformers/transformer.html

