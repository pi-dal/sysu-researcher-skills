# SYSU Researcher Skills

**SYSU institutional research access + selected open research extensions.**

AI agent skills for Sun Yat-sen University (SYSU) researchers and faculty, built on top of OpenCLI.

## Overview

This repository provides OpenCLI skills for academic research workflows. The skills are organized into two layers:

- **Core** — leverage SYSU's institutional subscriptions and library system.
- **Extension** — complement with open academic platforms for broader discovery.

## Prerequisites

- OpenCLI installed and configured.
- `opencli-plugin-sysu` and `opencli-plugin-webofscience` plugins installed.
- Chrome browser logged into Web of Science via SYSU's institutional access (for WoS skills).
- `opencli doctor` status green.

## Skills

### Core (SYSU institutional advantage)

| Skill | Description | Requires |
|-------|-------------|----------|
| `sysu-wos-literature-search` | Literature search on Web of Science, citation tracing (citing/cited papers), Result Analysis facet distribution, and institutional full-text retrieval. | SYSU WoS subscription |
| `sysu-wos-author-lookup` | Researcher profile lookups by name / ResearcherID / ORCID, tracking publication lists, h-index, and citation reports. | SYSU WoS subscription |
| `sysu-library-resource-access` | Searching physical/electronic collections in SYSU libraries, locating item holdings and call numbers, and checking SYSU subscriptions for specific databases (e.g. CNKI, IEEE Xplore). | SYSU Library access |

### Extension (open ecosystem)

| Skill | Description | Uses |
|-------|-------------|------|
| `sysu-open-literature-search` | Literature, preprint, and citation search on open academic platforms (arXiv, PubMed, Google Scholar, OpenAlex). | OpenCLI open adapters |
| `sysu-ai-model-data-search` | Querying trending ML models, datasets, spaces, and paper summaries on Hugging Face. | OpenCLI Hugging Face adapter |

## Usage

```bash
# Register skills locally
npx skills add .
```

## Scope

This repository focuses on researcher workflows — literature discovery, author profiling, resource access, and AI/data research. It deliberately does not cover student-facing workflows (course selection, grades, LMS study tools), which belong in separate skill sets.
