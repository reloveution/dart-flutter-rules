---
title: Hugging Face MCP Server
description: Models, datasets, papers, documentation, image gen
---

# Hugging Face MCP Server

## When to Use

- ML models, datasets, research papers
- Hugging Face documentation
- AI image generation (Flux 1 Schnell)

## When NOT to Use

- General web search (Firecrawl/web_search)
- Dart/Flutter packages (Dart MCP)

## Commands

**Models:** model_search (query, sort, limit, author, library, task)

**Datasets:** dataset_search (query, sort, tags)

**Papers:** paper_search (query, results_limit, concise_only)

**Spaces:** space_search

**Repo details:** hub_repo_details (repo_ids, repo_type)

**Docs:** hf_doc_search, hf_doc_fetch

**Image gen:** gr1_flux1_schnell_infer (prompt, width, height, num_inference_steps)

## Workflow

1. Discovery with filters → model_search/dataset_search
2. Details → hub_repo_details
3. Papers: concise_only for broad, false for specifics
4. HF docs: hf_doc_search → hf_doc_fetch
5. Image: defaults (4 steps, 1024x1024)
