# Example Prompts

Use these prompts to trigger `sysu-research-router` and its sub-skills for academic research workflows.

## Identifier-first lookups

- Find the paper behind DOI `10.1016/j.patter.2024.101046` and tell me whether it has an open-access full-text entry.
- Look up PubMed article `37780221` and summarize the title, authors, abstract, and MeSH terms.
- Fetch arXiv paper `2405.01234` and give me the abstract plus the PDF entry link.
- Open the Web of Science record for `WOS:001335131500001` and list the key metadata.

## Topic search

- Search recent PubMed results for `immune checkpoint inhibitor resistance` and give me the most relevant 5 papers.
- Search arXiv for recent work on `retrieval-augmented generation evaluation`.
- Do a cross-disciplinary search for `causal representation learning in biology` and start with the most structured public sources.
- Search SYSU library catalog for `天体物理` and find available copies.

## Researcher lookup

- Find the publication record for researcher named "李醒民" on Web of Science.
- Show me the h-index and citation report for this author profile.

## Citation and related-work tracing

- Starting from PMID `37780221`, show me related papers I should read next.
- Given this Web of Science UT, show me the citing articles and the reference list.
- Help me trace the citation chain around this paper and identify foundational works.

## Full-text access

- I have DOI `10.1016/j.patter.2024.101046`; find the best full-text entry link.
- For this paper, prefer public OA first and only fall back to browser-backed institutional sources if necessary.

## Literature-review support

- I am starting a literature review on `multimodal large language models in medical imaging`; collect representative papers grouped by source.
- I need a fast research reconnaissance on `graph neural networks for molecular property prediction`; use stable public sources first.
