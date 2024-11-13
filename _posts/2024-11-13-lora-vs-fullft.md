---
layout: post
title: Notes on the paper - LoRA vs Full Fine-Tuning: An Illusion of Equivalence
permalink: /posts/2024/11/13/lora-vs-fullft/
date: 2024-11-13
description:
tags: [lora, llm, interpretability]
categories: [lit-notes]
featured: true
---

My notes on the paper by Reece Shuttleworth, Jacob Andreas, Antonio Torralba, and Pratyusha Sharma. The paper was presented at NeurIPS 2024. The paper can be found [here](https://arxiv.org/pdf/2410.21228v1).

# First Pass
Are Full Fine-Tuning and LoRA equivalent?

- **Full Fine-Tuning** => Fine-tune the entire model on a new task.

- **LoRA** => Fine-tune only the adapter on a new task.

These have different structure considering their singular value decomposition (SVD) of the weight matrix. The paper shows that the two methods are not equivalent.

Fine-tuned models generalize outside the adaptation task's distribution but LoRA might have some problems with this. LoRA has **intruder dimensions**, as called by the authors, that are not seen in the full fine-tuning. LoRA with intruder dimensions might achieve comparable performance to full fine-tuning but when used with multiple tasks the performance drops.

**LoRA and full fine-tuning use different subspaces of the weight matrix.**

LoRA and full fiine-tuning have differences in neuron's angle and magnitude (Liu et al., 2024).

```bibtex
Shih-Yang Liu, Chien-Yi Wang, Hongxu Yin, Pavlo Molchanov, Yu-Chiang Frank Wang, KwangTing Cheng, and Min-Hung Chen. DoRA: Weight-Decomposed Low-Rank Adaptation. In Proceedings of the 41st International Conference on Machine Learning. International Conference on Machine Learning, 2024. URL https://arxiv.org/abs/2402.09353.
```

LoRA cannot match full fine-tuning in code generation, which is considered as a hard task (Biderman et al., 2024; Zhuo et al., 2024).

```bibtex
Dan Biderman, Jose Gonzalez Ortiz, Jacob Portes, Mansheej Paul, Philip Greengard, Connor Jennings, Daniel King, Sam Havens, Vitaliy Chiley, Jonathan Frankle, Cody Blakeney, and John P. Cunningham. LoRA Learns Less and Forgets Less. Transactions on Machine Learning Research, 2024. URL https://arxiv.org/abs/2405.09673.

Terry Yue Zhuo, Armel Zebaze, Nitchakarn Suppattarachai, Leandro von Werra, Harm de Vries, Qian Liu, and Niklas Muennighoff. Astraios: Parameter-Efficient Instruction Tuning Code Large Language Models, 2024. URL https://arxiv.org/abs/2401.00788.
```

It also has problems with long-form text generation (Ivison et al., 2023)

```bibtex
Hamish Ivison, Yizhong Wang, Valentina Pyatkin, Nathan Lambert, Matthew Peters, Pradeep Dasigi, Joel Jang, David Wadden, Noah A. Smith, Iz Beltagy, and Hannaneh Hajishirzi. Camels in a Changing Climate: Enhancing LM Adaptation with Tulu 2, 2023. URL https://arxiv. org/abs/2311.10702.
```

This paper aims to understand if these downsides of LoRA indicate a fundamental limitation of LoRA or if they can be addressed by better understanding the method.