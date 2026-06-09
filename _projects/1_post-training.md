---
layout: page
title: LLM Post-Training on Small-Scale Models
description: SFT, RLHF with process reward models, and latent-space knowledge distillation for improving mathematical reasoning in Qwen2.5-0.5B.
importance: 1
category: LLMs
---

Explored post-training techniques to improve mathematical reasoning in **Qwen2.5-0.5B** on GSM8K. We first fine-tuned the model via **SFT** and then via **RLHF** using format and outcome rewards. However, due to the sparse nature of outcome rewards, we observed the model over-optimizing the format reward, resulting in sub-optimal performance. To mitigate this, we employed **process reward models** that assign dense, step-level rewards to CoTs (chains-of-thought) rather than sparse outcome-based signals, improving test accuracy from **31% to 37%**.

Despite this improvement, we found that the model's CoTs remained poor — the model would repeat the question, heavily use LaTeX tags, or lose track of intermediate derived quantities. To address this, we replicated a **latent-space knowledge distillation** framework that transfers K latent reasoning tokens from Qwen2.5-7B (teacher) directly into the representation space of Qwen2.5-0.5B (student), bypassing traditional logit-based distillation.

Combining RLHF with this distillation approach achieved **41% test accuracy**, and we observed that the model's CoTs became significantly more concise and mathematically correct. This work demonstrates that augmenting RL-based post-training with representation-level knowledge transfer yields stronger reasoning in small-scale models.

Code: [Link](https://github.com/sabharwalrishabh/LLM-post-training)