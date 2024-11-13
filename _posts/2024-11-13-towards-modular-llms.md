---
layout: post
title: Notes on the paper - Towards Modular LLMs by Building and Reusing a Library of LoRAs
permalink: /posts/2024/11/13/towards-modular-llms/
date: 2024-11-13
description:
tags: [lora, llm, modular]
categories: [lit-notes]
featured: true
---

My notes on the paper by Oleksiy Ostapenko, Zhan Su, Edoardo Maria Ponti, Laurent Charlin, Nicolas Le Roux, Matheus Pereira, Lucas Caccia, and Alessandro Sordoni. The paper can be found [here](https://arxiv.org/pdf/2405.11157).

# First Pass
Parameter-efficient adaptations of LLMs are significant => Can we reuse trained adapters across tasks?

Model-based clustering (MBC) => Group tasks based on the similarity of their adapters. Find similarity (positive correlation) between LoRA weights of two tasks, and then transfer between those tasks.

Arrow => Dynamic selection of relevant adapters for a new task withoout retraining.

Previously few-shot adaptation with pretrained adapters was researched. This paper extends this idea to zero-shot adaptation.

For each task train an adapter is trained on multi-task data, then these adapters are mixed for unseen tasks.

# Second Pass

Private Adapters => For each task train a adapter.

Shared Adapter => Train a single adapter on all tasks. Might be problematic since the model cannot fit all tasks, (solution: increase the number of trainable parameters).

Poly/MHR Adapters => Combination of private and shared adapters.

**Model-Based Clustering (MBC)** => Create clusters of tasks and train one adapter per task cluster. 1. Train private LoRAs, 2. Group LoRA parameters into K clusters using K-means, 3. Train one adapter per cluster.

---

Mu Routing => LoRA adapters are linear, thus routing to exxisting experts could be done using uniform distribution. (the simplest method, average the weights of the adapters uniformly).

Arrow Routing => Estimating routing matrix by SVD(AB^T) and taking the right first singular vector, and compute the direction of most variance.

The paper used LoRA rank of 4, dropout of 0.05, learning rate of 1e-4, and MBC number of clusters of 10.

MBC and Arrow enhances the performance compared to Full Fine-Tuning.

# Third Pass
- Can we improve upon K-means clustering, and find the number of clusters automatically? Maybe using the semantics of the tasks (e.g. using the task descriptions).
- Can we also share parameters across clusters?

### References
```bibtex
@article{ostapenko2024towards,
  title={Towards modular llms by building and reusing a library of loras},
  author={Ostapenko, Oleksiy and Su, Zhan and Ponti, Edoardo Maria and Charlin, Laurent and Roux, Nicolas Le and Pereira, Matheus and Caccia, Lucas and Sordoni, Alessandro},
  journal={arXiv preprint arXiv:2405.11157},
  year={2024}
}
```