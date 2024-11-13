---
layout: post
title: Notes on the paper - LoRA vs Full Fine-Tuning:An Illusion of Equivalence
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

**LoRA and full fine-tuning use different subspaces of the weight matrix (intruder dimensions).**

**LoRA with intruder dimensions forgets pretraining distribution.**

LoRA and full fiine-tuning have differences in neuron's angle and magnitude (Liu et al., 2024).

```bibtex
Shih-Yang Liu, Chien-Yi Wang, Hongxu Yin, Pavlo Molchanov, Yu-Chiang Frank Wang, KwangTing Cheng, and Min-Hung Chen. DoRA: Weight-Decomposed Low-Rank Adaptation. In Proceedings of the 41st International Conference on Machine Learning. International Conference on Machine Learning, 2024. URL https://arxiv.org/abs/2402.09353.
```

LoRA cannot match full fine-tuning in code generation, which is considered as a hard task (Biderman et al., 2024; Zhuo et al., 2024). (Note: Biderman et al. (2024) also showed that setting a =  2r in LoRA improves results for higher ranks.)

```bibtex
Dan Biderman, Jose Gonzalez Ortiz, Jacob Portes, Mansheej Paul, Philip Greengard, Connor Jennings, Daniel King, Sam Havens, Vitaliy Chiley, Jonathan Frankle, Cody Blakeney, and John P. Cunningham. LoRA Learns Less and Forgets Less. Transactions on Machine Learning Research, 2024. URL https://arxiv.org/abs/2405.09673.

Terry Yue Zhuo, Armel Zebaze, Nitchakarn Suppattarachai, Leandro von Werra, Harm de Vries, Qian Liu, and Niklas Muennighoff. Astraios: Parameter-Efficient Instruction Tuning Code Large Language Models, 2024. URL https://arxiv.org/abs/2401.00788.
```

It also has problems with long-form text generation (Ivison et al., 2023)

```bibtex
Hamish Ivison, Yizhong Wang, Valentina Pyatkin, Nathan Lambert, Matthew Peters, Pradeep Dasigi, Joel Jang, David Wadden, Noah A. Smith, Iz Beltagy, and Hannaneh Hajishirzi. Camels in a Changing Climate: Enhancing LM Adaptation with Tulu 2, 2023. URL https://arxiv. org/abs/2311.10702.
```

This paper aims to understand if these downsides of LoRA indicate a fundamental limitation of LoRA or if they can be addressed by better understanding the method.

# Second Pass

First Aghajanyan et al. (2021) proposed the idea that LLMs has low instrinsic rank, so significantly less number of parameters are needed to have similar performance to full fine-tuning. This is the basis of LoRA.

```bibtex
Armen Aghajanyan, Sonal Gupta, and Luke Zettlemoyer. Intrinsic Dimensionality Explains the Effectiveness of Language Model Fine-Tuning. In Proceedings of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing (Volume 1: Long Papers). Association for Computational Linguistics, August 2021. URL https://aclanthology.org/2021.acl-long.568.
```

Sharma et al. (2024) showed that SVD of neuron's weight matrix can be used to understand fine-tuning's effect on pretrained weights.

```bibtex
Pratyusha Sharma, Jordan T. Ash, and Dipendra Misra. The Truth is in There: Improving Reasoning in Language Models with Layer-Selective Rank Reduction. In The Twelfth International Conference on Learning Representations, 2024. URL https://openreview.net/forum?id= ozX92bu8VA.
```

This paper uses this idea to see if LoRA and full fine-tuning's singular vectors in weight matrices are similar using to pretrained weights. They found out LoRA is not similar to pretrained singular vectors as full fine-tuning. Interestingly, with LoRA there are some singular vectors, **(intruder dimensions)**, that have very low cosine similarity to any pretrained singular vector.

**LoRA and full fine-tuning have differences in the changes they make to the pretrained weights.**

Authors find out that LoRA consistently contains intruder dimensions (rank <= 16, the number decreases when rank gets increased as LoRA starts to resemble full fine-tuning), and full fine-tuning almost never does. Hence, it can be stated that full fine-tuning is more similar to the pretrained model than LoRA.

**More fine-tuning data leads to more intruder dimensions in LoRA.**

---

LoRA has intruder dimensions that affect pretrained weights' impact. This is detrimental when using LoRA on tasks outside of the fine-tuning task's distribution.

---

# Third Pass
- Can we modify LoRA to prevent the formation of intruder dimensions while maintaining its parameter efficiency?
- How do intruder dimensions interact when multiple LoRA adapters are combined?

### References
```bibtex
@article{shuttleworth2024lora,
  title={LoRA vs Full Fine-tuning: An Illusion of Equivalence},
  author={Shuttleworth, Reece and Andreas, Jacob and Torralba, Antonio and Sharma, Pratyusha},
  journal={arXiv preprint arXiv:2410.21228},
  year={2024}
}
```