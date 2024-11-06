---
layout: post
title: Notes on the paper "What does BERT look at? An Analysis of BERT’s Attention (ACL 2019)"
date: 2024-11-06
description: My notes on the paper.
tags: [bert, attention, nlp]
categories: [research-notes]
featured: true
---

My notes on the paper by Kevin Clark, Urvashi Khandelwal, Omer Levy, and Christopher D. Manning. The paper was presented at ACL 2019. The paper can be found [here](https://arxiv.org/abs/1906.04341).

I do 3 passes of reading a paper. The first pass is to get a general idea of what the paper is about. The second pass is to understand the details of the paper. The third pass is to understand the paper in depth.

For this particular paper I did only the first pass because I wanted to understand the general idea of the paper.

# First Pass

1. **What is the problem?** The paper investigates what BERT attends to when making predictions.
2. **Why is it important?** Understanding what BERT or any other language model attends to is important as it can help us understand how these models **reason**.

### Abstract
Previous work focused on:
- Model outputs (final layer of the model)
- Internal vector representations (this could be the hidden states of the model)

BERT's attention heads focused on:
- Delimeter tokens (e.g. [CLS], [SEP])
- Some positional offsets, meaning that the attention heads are not just focusing on the token itself but also on the tokens around it.
- Or broadly on the entire sentence.

Some attention heads reflected already known linguistic phenomena:
- e.g. attention heads that focused on objects of verbs, coreference, etc.

### Conclusion
The paper proposed different methods to understand attention.

They state that in the attention maps linguistic knowledge can be found. They do something called **probing attention maps** to understand what the attention heads are focusing on.

So I believe the paper shown that BERT reflects linguistic phenomena in its attention heads. This is a very revealing insight into how BERT works.

### Introduction
Heads learn different types of information, in this case linguistic information. Language models like BERT by training on unlabeled data inherently learns linguistic information, thus there is no need for explicit linguistic features.

#### References
```bibtex
@article{clark2019does,
  title={What Does Bert Look At? An Analysis of Bert’s Attention},
  author={Clark, Kevin},
  journal={arXiv preprint arXiv:1906.04341},
  year={2019}
}
```