# RAG Pipeline Pattern

## Problem

Need reliable, grounded answers from a knowledge base.

## Pattern

Ingest -> chunk -> embed -> retrieve -> rerank -> generate -> evaluate.

## Example

Use hybrid retrieval and enforce a response format that cites retrieved evidence.

## When to Use / Avoid

Use for knowledge-heavy assistants. Avoid when deterministic lookup logic is enough.
