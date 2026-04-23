# docx2html Pipeline

## Overview

The current docx2html project is a Flask-based documentation production pipeline that combines DOCX conversion with a `webcontent` workflow. It produces normalized markdown, per-tutorial master files, and packaging outputs for publishing.

## Problem It Solves

- Source material is spread across tutorial web pages, ZIP assets, JSON payloads, and Word templates.
- Manual content assembly creates drift and inconsistent output structure.
- Publishing requires repeatable outputs with traceable intermediate artifacts.

## Architecture

- Flask UI plus job-driven API endpoints for long-running pipeline actions
- Core stages:
  1. `get_tutorial_assets.py`: discover tutorials, download ZIPs, extract JSON and Word assets
  2. `extract_k2container.py`: extract tutorial body content into `webcontent/extracted_html`
  3. Conversion: `docx -> html -> md` plus extracted HTML/TXT to markdown
  4. `build_master_docs.py`: build `webcontent/Master/*-master.md` from web markdown + docx markdown + JSON
  5. `Combine Masters`: generate `webcontent/Master/all-masters.md`
- Optional AI generation step creates `webcontent/ai_content/*-content.txt` (meta description + intro text)
- Docker runtime on port `8006` with mounted `input`, `output`, and `webcontent` volumes

## Key Decisions

- Keep deterministic conversion as the default path and use AI as an optional constrained pass.
- Preserve intermediate files (`master_inputs`, extracted assets, reports) for auditability and debugging.
- Add settings-based URL override mode to run targeted subsets instead of full tutorial batches.
- Separate cleanup and packaging into explicit operations to keep runs reproducible.

## Challenges

- Maintaining structure fidelity across DOCX, scraped web content, and JSON data.
- Handling inconsistent source formats and noisy embedded data (for example base64 image payloads).
- Balancing throughput with validation quality for batch documentation workflows.

## What I'd Improve

- Add stronger regression baselines for markdown structure and front matter consistency.
- Introduce per-template conversion heuristics for known edge cases.
- Add summary dashboards for job outcomes, warnings, and recurring failure categories.

## Notable Implementation Details

- Supports both full pipeline mode and direct folder conversion (`Docx` tab).
- Generates validation reports in `output/reports` for conversion quality checks.
- Adds front matter fields (`title`, `description`, `canonical_url`, `last_reviewed`) during master build.
- Includes cleanup for generated artifacts while preserving source code and settings.
- Supports downloadable outputs for markdown, master files, and AI content bundles.

## Optional OpenAI Summary Flow

When the user enables AI generation in Settings, the pipeline can call the OpenAI API to generate a concise summary package from markdown that has already been produced by earlier steps.

- Input: previously generated master markdown files in `webcontent/Master/*-master.md`
- Trigger: user turns on AI generation and runs the `AI Generate` action
- API configuration: `OPENAI_API_KEY` plus selected model (default configured as `gpt-4.1-mini`)
- Behavior: each master markdown file is processed individually and prompts request short summary-oriented content (for example, meta description and intro text)
- Output: generated summary content is written to `webcontent/ai_content/*-content.txt`

This keeps the core conversion deterministic while allowing an opt-in, API-based summarization pass for publishing-ready metadata and concise introductions.
