---
name: sysu-wos-literature-search
description: Search academic literature on Web of Science (WoS) using institutional subscription access, analyze results, trace citation networks, and retrieve full-text paths.
---

# sysu-wos-literature-search

## Overview

Use Clarivate Web of Science (WoS) via the OpenCLI `webofscience` plugin. Since SYSU subscribes to Web of Science, researchers can use this skill to perform literature searches, trace citation networks (citing and cited papers), analyze result distributions, and route to institutional full-text PDFs.

## Prerequisites

- Chrome browser logged into Web of Science via Sun Yat-sen University (SYSU) institutional access (e.g., library proxy or on-campus network).
- `opencli` core and `opencli-plugin-webofscience` installed.
- `opencli doctor` green for browser session state.

## Commands

### `opencli webofscience basic-search <query>`

Perform a basic keyword search in WoS.

**Arguments:**
- `query` (required, positional): The search query terms (e.g. topic, title, etc.).
- `--field` (optional): Field to search. Options include: `topic` (default), `title`, `author`, `publication_name`, `year`.
- `--limit` (optional): Maximum number of records to return (default is 10, max 50).

**Examples:**
```bash
opencli webofscience basic-search "perovskite solar cells" --limit 5
opencli webofscience basic-search "quantum key distribution" --field topic
```

### `opencli webofscience smart-search <query>`

Execute advanced queries using WoS fielded tags (e.g. TS=topic, TI=title, AU=author, OG=organization).

**Arguments:**
- `query` (required, positional): Fielded query string.
- `--limit` (optional): Maximum number of records to return (default is 10, max 50).

**Examples:**
```bash
# Search for articles on cancer immunotherapy published by Sun Yat-sen University authors
opencli webofscience smart-search "TS=(cancer immunotherapy) AND OG=(Sun Yat-sen University)" --limit 10

# Search for articles by a specific author in a specific topic
opencli webofscience smart-search "TS=(deep learning) AND AU=(LeCun Y)"
```

### `opencli webofscience record <id>`

Retrieve full metadata details (including abstract, categories, times cited, DOI) for a specific publication record.

**Arguments:**
- `id` (required, positional): WoS Accession Number (UT, prefixed with `WOS:`), DOI, or full WoS record URL.

**Examples:**
```bash
opencli webofscience record WOS:001335131500001
opencli webofscience record 10.1016/j.patter.2024.101046
```

### `opencli webofscience citing-articles <id>`

Retrieve a list of papers that have cited the target publication. Useful for forward citation tracking.

**Arguments:**
- `id` (required, positional): WoS UT identifier, DOI, or record URL.

**Examples:**
```bash
opencli webofscience citing-articles 10.1016/j.patter.2024.101046 --limit 5
```

### `opencli webofscience references <id>`

Retrieve the bibliography (list of cited references) for a target publication. Useful for backward citation tracking.

**Arguments:**
- `id` (required, positional): WoS UT identifier, DOI, or record URL.

**Examples:**
```bash
opencli webofscience references WOS:001335131500001 --limit 10
```

### `opencli webofscience analyze-results <query>`

Analyze search results by facet distribution (such as Web of Science Categories, Publication Years, Document Types, etc.).

**Arguments:**
- `query` (required, positional): Query keywords or fielded query.
- `--field` (optional): Field to search for the base query (default is `topic`).

**Examples:**
```bash
opencli webofscience analyze-results "solid-state battery" --field topic
```

### `opencli webofscience full-text <id-or-doi>`

Find the institutional full-text URL path (publisher routing) for a specific paper.

**Arguments:**
- `id-or-doi` (required, positional): WoS UT identifier or DOI.

**Examples:**
```bash
opencli webofscience full-text WOS:001335131500001
opencli webofscience full-text 10.1016/j.patter.2024.101046
```

## Workflows

### 1. Topic Exploration and Citation Tracking
Search for high-impact literature in a topic, examine the top record, find its citations, and route to full-text PDF:
```bash
# 1. Search for a specific research topic
opencli webofscience basic-search "graph neural networks" --limit 5

# 2. Get details and UT code for the most cited paper
opencli webofscience record WOS:000523456700001

# 3. Find recent papers citing it to trace new developments
opencli webofscience citing-articles WOS:000523456700001 --limit 5

# 4. Get the publisher URL to download the full text
opencli webofscience full-text WOS:000523456700001
```

### 2. Affiliation and Field Analysis
Track publications in a particular field authored by researchers from Sun Yat-sen University (SYSU):
```bash
# 1. Search using organization and topic tags
opencli webofscience smart-search "OG=(Sun Yat-sen University) AND TS=(single-cell RNA sequencing)" --limit 10
```
