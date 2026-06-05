# SYSU Researcher Skills

AI agent skills for Sun Yat-sen University (SYSU) researchers and faculty, built on top of OpenCLI.

## Overview

This repository provides OpenCLI skills tailored for academic researchers at SYSU. It leverages SYSU's subscription to Clarivate Web of Science (WoS) and the SYSU Library system to enable autonomous search, tracking, and retrieval of research literature and researcher profiles.

## Prerequisites

- OpenCLI installed and configured.
- `opencli-plugin-sysu` and `opencli-plugin-webofscience` plugins installed.
- Chrome browser logged into Web of Science (wos) using SYSU's institutional access.
- `opencli doctor` status green.

## Skills

- **`sysu-wos-literature-search`**: Literature search on Web of Science, citation tracing (citing/cited papers), Result Analysis facet distribution, and institutional full-text retrieval.
- **`sysu-wos-author-lookup`**: Researcher profile lookups by name/ResearcherID/ORCID, tracking publication lists, h-index, and citation reports.
- **`sysu-library-resource-access`**: Searching physical/electronic collections in SYSU libraries, locating item holding locations and call numbers, and checking SYSU subscriptions for specific databases (e.g., CNKI, IEEE Xplore).

## Usage

```bash
# Register skills locally
npx skills add .
```
