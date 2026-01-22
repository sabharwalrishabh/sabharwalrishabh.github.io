---
layout: page
title: FastAPI Safety Gateway
description: Guardrails + agentic safety loop for a vLLM-served Llama-3.1-8B-Instruct.
importance: 1
category: systems
---

Built a safety gateway around a vLLM-served **Llama-3.1-8B-Instruct**, combining learned and rule-based checks:

- **Multi-label toxicity/harm classification** (toxic-bert)
- **Prompt-injection detection** (local detector)
- **PII detection and anonymization** (Microsoft Presidio)

I also implemented an **agentic safety loop** that:
1) rewrites risky prompts,
2) repairs unsafe outputs through policy-conditioned re-prompting,
3) exposes user-tunable thresholds, custom deny-lists, and end-to-end decision traces (CLI + Streamlit UI).

Code: https://github.com/sabharwalrishabh/Safety-Guardrails-for-LLMs
