---
name: sysu-reference-retrieval
description: Retrieve full bibliographic records and item details from SYSU Library catalog.
---

# sysu-reference-retrieval

## Overview

Retrieve detailed bibliographic records, call numbers, locations, and availability for specific items in the SYSU Library catalog using OpenCLI SYSU plugin commands.

## Prerequisites

- Chrome logged into SYSU Library (library.sysu.edu.cn)
- `opencli doctor` green for COOKIE adapters
- `opencli-plugin-sysu` installed

## Commands

### `opencli sysu library-item <catalog-url-or-id>`

Get full record details for a specific catalog item.

**Arguments:**
- `catalog-url-or-id` (required, positional): INNOPAC detail URL or catalog record ID

**Examples:**
```
opencli sysu library-item "https://library.sysu.edu.cn/record=b1234567"
opencli sysu library-item "b1234567"
```

## Workflows

### Retrieve a book record after a catalog search

```
opencli sysu library-catalog "相对论" --type subject
```
Pick the relevant record ID from the catalog results, then:
```
opencli sysu library-item <record-id>
```

### Get full metadata for a known item

```
opencli sysu library-item "b1234567"
```

## Notes

- `library-item` returns full INNOPAC record: title, author, publisher, ISBN, call number, location, availability
- Record ID format: typically `b` followed by 7 digits
- Combine with `sysu-literature-search` for full research workflow
