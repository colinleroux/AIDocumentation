# Evaluation

## How I Test RAG Systems

- Build a representative query set
- Score retrieval relevance before answer quality
- Check groundedness against retrieved evidence
- Track failure categories over time

## Common Failure Cases

- Confident but unsupported answers
- Missing key chunk in top-k retrieval
- Wrong source selected due to lexical noise

## Metrics That Matter

- Top-k relevance quality
- Grounded answer rate
- Citation usefulness
- Latency and cost per request
