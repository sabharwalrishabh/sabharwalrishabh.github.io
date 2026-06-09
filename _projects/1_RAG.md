---
layout: page
title: Multi-Step Agentic RAG System for Multi-Hop QA
description: Decoupled agentic RAG pipeline with multi-step retrieval over 270K facts from HotpotQA.
importance: 2
category: LLMs
---

- Built a multi-hop QA system over **270K facts** from HotpotQA, benchmarking sparse (BM25), dense (BAAI/bge-base-en-v1.5 + FAISS), and hybrid (Reciprocal Rank Fusion) retrieval strategies with **cross-encoder reranking** as the final stage — improving Recall@5 from 0.46 to 0.78 and EM@5 from 0.16 to 0.57. - Served the pipeline via **FastAPI** with **vLLM**-hosted Qwen3-8B and GPT-4.1-mini for inference.
- Single-step RAG with top-5 cross-encoder facts achieved an EM of 0.56, but HotpotQA's multi-hop structure means certain supporting facts can only be surfaced after identifying intermediate entities from earlier retrieved facts. - A unified agentic approach where a single LLM retrieved and answered within the same multi-turn context — degraded to 0.53 EM, as growing conversation history caused verbose, format-violating answers.

To address this, I designed a **decoupled agentic RAG system**:
1. A **retrieval agent** performs multi-step retrieval via LLM tool calling to gather additional evidence.
2. All collected facts are passed to a clean **answer-generation agent** with no tool-calling history.

This achieved **0.67 EM** and **0.79 F1**. Error analysis using GPT-4.1 as a judge revealed that of 33 failures, only 12 were genuinely incorrect — the remaining 21 were penalised solely by EM's strict surface-level matching.

Code: [Link](https://github.com/sabharwalrishabh/rag)