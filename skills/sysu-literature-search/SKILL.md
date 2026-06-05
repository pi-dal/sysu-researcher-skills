---
name: sysu-literature-search
description: Search SYSU Library catalog and databases for research literature, books, and academic resources.
---

# sysu-literature-search

## Overview

Search Sun Yat-sen University's Library system using OpenCLI SYSU plugin commands. This skill helps researchers discover print and electronic collections, browse subscribed databases, and locate resources.

## Prerequisites

- Chrome logged into SYSU Library (library.sysu.edu.cn)
- `opencli doctor` green for COOKIE adapters
- `opencli-plugin-sysu` installed

## Commands

### `opencli sysu library-catalog <query>`

Search the library catalog for books, journals, and other collections.

**Arguments:**
- `query` (required, positional): Search keyword
- `--type` (optional): Search type — `title` (default), `author`, `subject`, `isbn`, `all`

**Examples:**
```
opencli sysu library-catalog "algorithm design" --limit 5
opencli sysu library-catalog "天体物理" --type subject
opencli sysu library-catalog "9787115511016" --type isbn
opencli sysu library-catalog "李醒民" --type author
```

### `opencli sysu library-databases [keyword]`

Browse and filter SYSU subscribed academic databases.

**Arguments:**
- `keyword` (optional, positional): Filter databases by keyword

**Examples:**
```
opencli sysu library-databases
opencli sysu library-databases "Web of Science"
opencli sysu library-databases "CNKI"
```

## Workflows

### Find a book and check availability

```
opencli sysu library-catalog "机器学习" --type subject
```
Review results, pick a relevant title, then:
```
opencli sysu library-item <record-id>
```

### Discover relevant databases for a field

```
opencli sysu library-databases "mathematics"
opencli sysu library-databases "化学"
```

## Notes

- Library catalog searches return print/electronic collection records with location and availability
- Database listings include access URLs and descriptions
- Both commands require an active Chrome session logged into SYSU Library
