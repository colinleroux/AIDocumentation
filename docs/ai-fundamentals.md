# AI Engineering Fundamentals

## What is AI Engineering (Practical View)

AI engineering is product engineering with probabilistic components. The goal is not just "make the model answer" but "make the system reliable, useful, and maintainable."

## LLM Basics (Only What Matters in Practice)

- LLMs are pattern predictors, not truth engines
- Prompt quality directly affects output quality
- Retrieval quality often matters more than prompt cleverness
- Guardrails and validation are part of the product, not optional extras

## Tokens, Context, and Limitations

- Tokens are cost, latency, and capacity units
- Context windows are limited, so selection is everything
- Bigger prompts can reduce clarity when irrelevant content is included

## Embeddings Explained Simply

Embeddings convert text into vectors so we can search by meaning instead of exact wording.

## Retrieval vs Fine-Tuning vs Prompting

- Prompting: first step for behavior shaping
- Retrieval (RAG): best for fresh, private, or large knowledge
- Fine-tuning: useful when style/behavior consistency is required at scale

## When NOT to Use AI

Skip AI when deterministic rules solve the task better, correctness must be exact every time, or operational risk outweighs value.
