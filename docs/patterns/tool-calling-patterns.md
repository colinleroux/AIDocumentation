# Tool Calling Patterns

## Problem

Tool orchestration fails when schemas are loose and validation is weak.

## Pattern

Define strict tool schemas, validate arguments, add retries for transient failures, and provide fallbacks.

## Example

Planner selects tool -> validator checks args -> executor runs tool -> summarizer composes final response.

## When to Use / Avoid

Use in multi-step assistants. Avoid when a direct model response is simpler and sufficient.
