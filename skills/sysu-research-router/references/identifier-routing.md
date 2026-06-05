# Identifier Routing Reference

## Decision order

1. **DOI** → `opencli openalex work <doi>` — fastest structured metadata + open-access URL
2. **PMID** → `opencli pubmed article <pmid>` — authoritative PubMed record
3. **arXiv ID** → `opencli arxiv paper <id>` — direct preprint + PDF entry
4. **WOS UT** → `opencli webofscience record <ut>` — full Web of Science record
5. **Full text with DOI** → `opencli openalex work <doi>` first, then `opencli webofscience full-text` if OA missing
6. **Full text with WOS UT only** → `opencli webofscience full-text <ut>`

## Practical examples

| Identifier | Route | Why |
|---|---|---|
| `10.1016/j.patter.2024.101046` | `opencli openalex work 10.1016/j.patter.2024.101046` | Best structured metadata + OA entry first |
| `37780221` | `opencli pubmed article 37780221` | Native PubMed record, biomedical authority |
| `2405.01234` | `opencli arxiv paper 2405.01234` | Direct preprint record with PDF entry |
| `WOS:001335131500001` | `opencli webofscience record WOS:001335131500001` | Native WoS record and browser-backed full context |

## Escalation rules

- Do not start with Web of Science if a stable public identifier route already answers the question.
- Use Web of Science when the task explicitly needs authoritative citation networks, institution-backed full-text links, or a native WoS UT record.
- If the user only gives a topic, do not guess an identifier route. Use domain-aware search first.

## Failure boundaries

- If OpenAlex returns metadata but no `openAccessUrl`, say so clearly and escalate only if browser-backed sources are justified.
- If CNKI, Wanfang, or Web of Science depend on a logged-in browser session, say so before relying on them.
- If no route yields a result, report that plainly instead of fabricating a paper match.
