# Flask AI App Structure Pattern

## Problem

AI app code becomes brittle when routing, prompting, model calls, and data access are mixed.

## Pattern

Separate concerns: routes, orchestration services, model adapters, retrieval/data layer, and evaluation helpers.

## Example

`/chat` route calls an orchestrator, which gets context from retrieval and selects a model adapter.

## When to Use / Avoid

Use for production paths. Avoid excessive structure in quick throwaway prototypes.
