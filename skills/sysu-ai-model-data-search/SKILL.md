---
name: sysu-ai-model-data-search
description: Track and retrieve top AI/ML models, datasets, spaces, and papers from Hugging Face via OpenCLI.
---

# sysu-ai-model-data-search

## Overview

Retrieve details on open-source machine learning models, datasets, demo spaces, and community-discussed papers from Hugging Face via the OpenCLI `hf` plugin. This skill helps AI/ML researchers keep track of trending resources, download counts, and paper summaries.

## Prerequisites

- `opencli` core installed.
- Internet connectivity to query the Hugging Face API.

## Commands

### `opencli hf models`

Retrieve trending, top-liked, or top-downloaded machine learning models.

**Options:**
- `--sort` (optional): Sorting criteria. Options include `downloads`, `likes`, `trending`, `freshness`.
- `--limit` (optional): Maximum number of models to return (default 10).
- `--search` (optional): Filter models by name/keyword.

**Examples:**
```bash
# List top 5 trending models
opencli hf models --sort trending --limit 5

# Search for LLaMA-related models sorted by downloads
opencli hf models --search "llama" --sort downloads --limit 10
```

### `opencli hf datasets`

Retrieve top or trending datasets on Hugging Face.

**Options:**
- `--sort` (optional): Sorting criteria. Options include `downloads`, `likes`, `trending`, `freshness`.
- `--limit` (optional): Maximum number of datasets to return (default 10).
- `--search` (optional): Filter datasets by name/keyword.

**Examples:**
```bash
# List top downloaded datasets
opencli hf datasets --sort downloads --limit 5

# Search for image-related datasets
opencli hf datasets --search "image" --sort downloads
```

### `opencli hf spaces`

Retrieve top demo spaces hosted on Hugging Face Spaces.

**Options:**
- `--sort` (optional): Sorting criteria. Options include `likes`, `created_at`, `last_modified`.
- `--limit` (optional): Maximum number of spaces to return.
- `--search` (optional): Filter spaces by name/keyword.

**Examples:**
```bash
# List top 10 most liked demo spaces
opencli hf spaces --sort likes --limit 10
```

### `opencli hf top`

Get the list of daily top upvoted papers on Hugging Face Daily Papers.

**Options:**
- `--limit` (optional): Number of papers to retrieve (default 10).

**Examples:**
```bash
opencli hf top --limit 5
```

### `opencli hf paper <id>`

Retrieve full metadata, abstract summary, author list, and community-extracted AI keywords for a paper by its arXiv ID.

**Arguments:**
- `id` (required, positional): The arXiv ID of the paper.

**Examples:**
```bash
opencli hf paper 2302.13971
```

---

## Workflows

### 1. Trend Tracking and Resource Discovery
Discover trending models, locate their corresponding dataset resources, and read the paper:
```bash
# 1. Look up the top trending models
opencli hf models --sort trending --limit 5

# 2. Check the daily top papers on Hugging Face to see what's being discussed
opencli hf top --limit 5

# 3. Pull details and keywords for a specific paper by its arXiv ID
opencli hf paper 2310.06825
```
