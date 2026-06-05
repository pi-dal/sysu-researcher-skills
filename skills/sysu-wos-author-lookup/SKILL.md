---
name: sysu-wos-author-lookup
description: Query academic profiles, trace researcher h-index, analyze publication metrics, and search for researcher profiles by name or ID on Web of Science.
---

# sysu-wos-author-lookup

## Overview

Retrieve details about researchers, their profiles, publication lists, h-index, and citation reports from Clarivate Web of Science (WoS) using OpenCLI `webofscience` plugin.

## Prerequisites

- Chrome browser logged into Web of Science via Sun Yat-sen University (SYSU) institutional access.
- `opencli` core and `opencli-plugin-webofscience` installed.
- `opencli doctor` green for browser session state.

## Commands

### `opencli webofscience author-search <query>`

Search for researcher profiles by author name (e.g. "Last Name, First Name" or "First Last").

**Arguments:**
- `query` (required, positional): Researcher name query.

**Examples:**
```bash
opencli webofscience author-search "Yann LeCun"
opencli webofscience author-search "Shu-Hong Yu"
```

### `opencli webofscience author-record <id>`

Retrieve a researcher's profile details, including their current organization affiliation, h-index, total citations, and publication lists by Web of Science ResearcherID or ORCID.

**Arguments:**
- `id` (required, positional): Researcher ID or ORCID.

**Examples:**
```bash
# Query researcher record using ResearcherID
opencli webofscience author-record F-1234-2011

# Query researcher record using ORCID
opencli webofscience author-record 0000-0002-1234-5678
```

### `opencli webofscience citation-report <query>`

Generate a citation report showing aggregate metrics (h-index, average citations per item, citation count over time) for a group of publications matching a query.

**Arguments:**
- `query` (required, positional): Query terms representing a author or topic.
- `--field` (optional): Field to search (default `topic`).

**Examples:**
```bash
# Generate citation report for publications by an author (using AU= tag in smart search query is best)
opencli webofscience citation-report "AU=(LeCun Y)" --field author
```

## Workflows

### 1. Identify a Researcher and Retrieve their Publication Metrics
Search for a researcher's profile by name, grab their Researcher ID, and fetch their publication details:
```bash
# 1. Search for author by name
opencli webofscience author-search "Schmidhuber Juergen"

# 2. Get their full profile and list of publications using their ResearcherID / ORCID
opencli webofscience author-record 0000-0002-1234-5678
```

### 2. Generate Citation Metrics for a specific SYSU research group
```bash
# Generate a citation report for a specific author and affiliation
opencli webofscience citation-report "AU=(Wang Y) AND OG=(Sun Yat-sen University)" --field topic
```
