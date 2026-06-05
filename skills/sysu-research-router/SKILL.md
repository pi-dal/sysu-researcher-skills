---
name: sysu-research-router
description: Meta-skill for academic research routing — identifier-first lookup, source-priority guidance, and delegation to domain sub-skills.
---

# Academic Research Router

Meta-skill that routes academic research queries to the right source and skill based on input type and research intent.

## Overview

This skill is the entry point for academic research queries. Instead of guessing which source to use, it follows deterministic routing rules:

- **Identifier-first**: DOI / PMID / arXiv ID / WOS UT each have a canonical source
- **Public-first**: Use open sources (OpenAlex, PubMed, arXiv) before institution-gated ones (Web of Science)
- **Domain-aware**: Biomedical topics route differently from CS topics

## Routing rules

| Input | Primary route | Alternative |
|-------|--------------|-------------|
| DOI | `opencli openalex work <doi>` | `opencli webofscience full-text <doi>` |
| PMID | `opencli pubmed article <pmid>` | — |
| arXiv ID | `opencli arxiv paper <id>` | — |
| WOS UT | `opencli webofscience record <ut>` | — |
| Biomedical topic | `opencli pubmed search` | `opencli arxiv search` |
| CS / ML topic | `opencli arxiv search` | `opencli openalex search` |
| General topic | `opencli openalex search` | `opencli arxiv search` / `opencli google-scholar search` |
| Chinese paper | `opencli cnki search` / `opencli wanfang search` (login required) | — |
| Citation tracing | `opencli webofscience citing-articles` / `opencli webofscience references` | — |
| Full text | `opencli openalex work <doi>` | `opencli webofscience full-text` |
| Author profile | `opencli dblp author` / `opencli arxiv author` | `opencli webofscience author-search` / `opencli wos author-record` |

## Sub-skills

After determining the route, delegate to the appropriate sub-skill:

**Core (SYSU institutional advantage):**
- `sysu-wos-literature-search`: WoS search, citation tracing, result analysis, full-text retrieval
- `sysu-wos-author-lookup`: Researcher profiles, h-index, citation reports
- `sysu-library-resource-access`: SYSU library catalog, database subscriptions, item details

**Extension (open ecosystem):**
- `sysu-open-literature-search`: arXiv, PubMed, Google Scholar, OpenAlex
- `sysu-ai-model-data-search`: Hugging Face models, datasets, spaces

## Source priority

1. **openalex** — most stable public structured metadata, strongest default first hop for DOI + OA entry routing
2. **pubmed / arxiv** — domain-specialized, public, stable
3. **webofscience** — browser-backed and slower, but valuable for authoritative citation and full-record workflows
4. **google-scholar** — broad coverage but more fragile due to anti-scraping
5. **cnki / wanfang** — useful for Chinese scholarly search, but login-dependent

## Escalation rules

1. Do not start with Web of Science if a public route already answers the query
2. Use Web of Science when the task needs: authoritative citation networks, institution-backed full-text links, native WoS UT records
3. If OpenAlex returns metadata but no `openAccessUrl`, escalate only if browser-backed sources are justified
4. If all routes fail, report clearly instead of fabricating results

## Known limits

- `webofscience` commands are browser-backed, slower (often 10-30s), and more brittle if the browser/CDP session is unstable
- `cnki` and `wanfang` require a logged-in browser session and may fail after session expiry
- `google-scholar` may trigger CAPTCHA or throttling under repeated use
- `openalex` can return metadata and OA entry URLs, but not every record has open-access full text
- This skill is read-only: no posting, commenting, following, downloading workflows, or state-changing platform actions
- SYSU WoS and Library access require an active institutional login session
- If no source returns results, say so clearly; do not invent titles, authors, abstracts, or citation data

## Preferred commands by intent

### Paper search

```bash
opencli pubmed search
opencli arxiv search
opencli openalex search
opencli google-scholar search
```

### Single-record detail

```bash
opencli openalex work <doi>
opencli pubmed article <pmid>
opencli arxiv paper <id>
opencli webofscience record <ut>
```

### Citation tracing

```bash
opencli pubmed citations <pmid>
opencli pubmed related <pmid>
opencli webofscience citing-articles <ut>
opencli webofscience references <ut>
```

### Full-text access

```bash
opencli openalex work <doi>
opencli webofscience full-text <ut-or-doi>
```

### Author lookup

```bash
opencli arxiv search --query "author:<name>"
opencli pubmed search --query "<name>[Author]"
opencli webofscience author-search --name "<name>"
opencli webofscience author-record --id "<researcher-id>"
```

## Examples

See [examples/prompts.md](examples/prompts.md) for full prompt examples.

### Identifier lookups

```
DOI → opencli openalex work 10.1016/j.patter.2024.101046
PMID → opencli pubmed article 37780221
arXiv → opencli arxiv paper 2405.01234
WOS UT → opencli webofscience record WOS:001335131500001
```

### Topic search

```
Biomedical: opencli pubmed search --query "immune checkpoint inhibitor resistance"
CS: opencli arxiv search --query "retrieval-augmented generation evaluation"
Cross-discipline: opencli openalex search --query "causal representation learning in biology"
```

See [references/identifier-routing.md](references/identifier-routing.md) for full routing reference.
