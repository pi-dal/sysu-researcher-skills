---
name: sysu-open-literature-search
description: Search academic literature, preprints, and citations using open platforms like arXiv, PubMed, Google Scholar, and OpenAlex via OpenCLI.
---

# sysu-open-literature-search

## Overview

Use open and free global academic databases and preprints index engines via OpenCLI to search literature, inspect paper abstracts/details, trace author profiles, and generate citations. Platforms included are: arXiv, PubMed, Google Scholar, and OpenAlex.

## Prerequisites

- `opencli` core installed.
- Internet connectivity to query open academic APIs.
- Chrome browser for Google Scholar adapter operations (managed automatically by OpenCLI).

## Commands

### arXiv (`opencli arxiv`)

Query preprint papers and author records in computer science, physics, mathematics, and related fields.

#### `opencli arxiv search <query>`
Search for arXiv papers by keyword, title, or abstract.
- **Example**: `opencli arxiv search "LoRA fine-tuning" --limit 5`

#### `opencli arxiv paper <id>`
Retrieve details of a specific paper by its arXiv ID.
- **Example**: `opencli arxiv paper 2106.09685`

#### `opencli arxiv author <author>`
List arXiv papers by a given author (newest first).
- **Example**: `opencli arxiv author "Ilya Sutskever"`

#### `opencli arxiv recent <category>`
List recent arXiv submissions in a specific category (e.g., `cs.CL`, `cs.CV`, `stat.ML`).
- **Example**: `opencli arxiv recent cs.CL --limit 10`

---

### PubMed (`opencli pubmed`)

Query biomedical and life sciences literature from the National Institutes of Health (NIH).

#### `opencli pubmed search <query>`
Search for PubMed articles with advanced filters.
- **Example**: `opencli pubmed search "crispr gene editing" --limit 5`

#### `opencli pubmed article <pmid>`
Get detailed metadata, authors, and abstract for a PubMed article by its PMID.
- **Example**: `opencli pubmed article 32425712`

#### `opencli pubmed author <name>`
Search PubMed articles by author name and optional affiliation.
- **Example**: `opencli pubmed author "Jennifer Doudna"`

#### `opencli pubmed citations <pmid>`
Retrieve citation relationships (cited by and references) for a PubMed article.
- **Example**: `opencli pubmed citations 32425712`

---

### Google Scholar (`opencli google-scholar`)

Search across a wide range of academic disciplines and sources, and retrieve author profiles.

#### `opencli google-scholar search <query>`
Perform a standard Google Scholar search.
- **Example**: `opencli google-scholar search "Attention is all you need"`

#### `opencli google-scholar profile <author>`
View a scholar's Google Scholar profile to inspect h-index, total citations, and public publications.
- **Example**: `opencli google-scholar profile "Geoffrey Hinton"`

#### `opencli google-scholar cite <query>`
Retrieve pre-formatted citation styles (APA, MLA, BibTeX, etc.) for a paper matching the query.
- **Example**: `opencli google-scholar cite "ResNet Deep Residual Learning"`

---

### OpenAlex (`opencli openalex`)

Query a massive, open catalog of global research works, authors, and venues.

#### `opencli openalex search <query>`
Search OpenAlex works (papers, books, preprints) by keyword.
- **Example**: `opencli openalex search "contrastive language-image pre-training"`

#### `opencli openalex work <id>`
Fetch details and abstract of a specific work by its OpenAlex ID or DOI.
- **Example**: `opencli openalex work W4289895066`

---

## Workflows

### 1. Cross-Platform Topic Exploration
Search arXiv and PubMed for a topic, and get citation details:
```bash
# 1. Search recent arXiv preprints on single-cell LLMs
opencli arxiv search "single-cell large language model" --limit 5

# 2. Search PubMed for peer-reviewed papers on the same topic
opencli pubmed search "single-cell transformer" --limit 5

# 3. Retrieve the full details of a promising paper from PubMed
opencli pubmed article 38165789
```

### 2. Researcher Scholarly Profile Analysis
Check an author's profile on Google Scholar and find their preprints on arXiv:
```bash
# 1. Check Google Scholar h-index and citation trajectory
opencli google-scholar profile "Yann LeCun"

# 2. View recent arXiv submissions by the same researcher
opencli arxiv author "Yann LeCun" --limit 5
```
