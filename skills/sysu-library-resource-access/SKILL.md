---
name: sysu-library-resource-access
description: Verify SYSU Library subscriptions for academic databases, search the catalog for research materials, and retrieve item locations and availability.
---

# sysu-library-resource-access

## Overview

Access Sun Yat-sen University (SYSU) Library resources using OpenCLI `sysu` plugin commands. This skill is optimized for researchers to verify if SYSU subscribes to specific academic databases, find print research materials in campus libraries, and check item details.

## Prerequisites

- `opencli` core and `opencli-plugin-sysu` installed.
- Access to the internet (no login required for public library catalog metadata; some database proxy access may require campus VPN or authentication).

## Commands

### `opencli sysu library-databases [query]`

Browse and filter academic databases subscribed to by SYSU. Very useful to verify if database portals (e.g., IEEE Xplore, CNKI, Web of Science) are accessible via SYSU library networks.

**Arguments:**
- `query` (optional, positional): Keyword to filter the database list.

**Examples:**
```bash
# List all databases
opencli sysu library-databases

# Search for a specific Chinese database
opencli sysu library-databases "CNKI"

# Search for a specific foreign database
opencli sysu library-databases "IEEE Xplore"
```

### `opencli sysu library-catalog <query>`

Search the library catalog for books, research journals, reference materials, or proceedings.

**Arguments:**
- `query` (required, positional): The search keywords.
- `--type` (optional): Search type — `title` (default), `author`, `subject`, `isbn`, `all`.
- `--limit` (optional): Max results to return.

**Examples:**
```bash
opencli sysu library-catalog "advanced quantum mechanics" --limit 5
opencli sysu library-catalog "Shu-Hong Yu" --type author
```

### `opencli sysu library-item <record-id>`

Retrieve a detailed bibliographic record, campus locations, call numbers, and real-time loan/holding availability status for a specific catalog item.

**Arguments:**
- `record-id` (required, positional): The INNOPAC record ID (e.g., `b1234567`) or detail URL.

**Examples:**
```bash
opencli sysu library-item "b2345678"
opencli sysu library-item "https://library.sysu.edu.cn/record=b2345678"
```

## Workflows

### 1. Verify Database Access
Before starting literature search on a new platform, verify if SYSU has a subscription and get the entry point link:
```bash
opencli sysu library-databases "PubMed"
# Output will display database description and the institutional entry URL
```

### 2. Locate a Print Research Monograph
When a researcher needs to reference or borrow a physical copy of a key monograph:
```bash
# 1. Search the title in the catalog
opencli sysu library-catalog "The Glass Bead Game" --limit 5

# 2. Use the record ID (e.g., b2398456) to retrieve holding details and shelf location
opencli sysu library-item "b2398456"
# Output shows campus location (e.g., 东校园图书馆, 南校园总馆), Call Number, and Availability (e.g., "On Shelf")
```
