# MVP Internal RAG

## Overview

MVP Internal RAG is a containerized internal AI support assistant built to run fully in-house. It provides grounded, citation-backed answers from internal documentation using a local model stack.

## Problem It Solves

- Internal support knowledge was spread across markdown, text, and PDF sources.
- Answers needed to be traceable to source documents, not just generated from model memory.
- The solution needed to run without relying on external AI APIs.

## Architecture

- Service stack: Flask/FastAPI app + Ollama + Qdrant via Docker Compose
- Ingestion flow: load docs -> chunk text -> embed chunks -> upsert into Qdrant
- Query flow: embed question -> retrieve candidates -> rerank -> generate grounded answer
- UI/API supports retrieval controls such as `top_k`, strictness, score thresholds, and answer style

## Key Decisions

- Use RAG over fine-tuning for maintainability and faster iteration.
- Keep models local (`dolphin3` for generation, `nomic-embed-text` for embeddings).
- Enforce source-aware responses with explicit citation formatting.
- Add strict mode and minimum semantic threshold to reduce weak-context answers.

## Challenges

- Balancing recall and precision for documentation-heavy queries.
- Keeping chunk size and overlap effective across different document formats.
- Preventing plausible but weakly supported responses in edge cases.

## What I'd Improve

- Add automated regression tests for retrieval and answer quality.
- Expand observability on retrieval misses and reranking behavior.
- Introduce per-document chunking profiles for better retrieval consistency.

## Notable Implementation Details

- Endpoints include `/ingest`, `/chat`, `/ask`, `/find`, and `/health`.
- Supports page-aware citations for PDF-derived chunks.
- Uses deterministic point IDs for stable Qdrant upserts.
- Containerized deployment supports local GPU acceleration where available.
