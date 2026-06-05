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

## Escalation rules

1. Do not start with Web of Science if a public route already answers the query
2. Use Web of Science when the task needs: authoritative citation networks, institution-backed full-text links, native WoS UT records
3. If OpenAlex returns metadata but no `openAccessUrl`, escalate only if browser-backed sources are justified
4. If all routes fail, report clearly instead of fabricating results

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
