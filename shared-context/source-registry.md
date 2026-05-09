# Source Registry

Endpoints, query templates, and operational notes for the three sources the paper-synthesizer agent reads each week. This file is read by the agent during the run; you only edit it if a source's API actually changes.

---

## bioRxiv

**Endpoint (date window):**
```
https://api.biorxiv.org/details/biorxiv/{YYYY-MM-DD}/{YYYY-MM-DD}/{cursor}
```

- `cursor` is the offset into the result set; pages are 100 records.
- No auth, no rate-limit-key. Be polite — ~1 req/sec is safe.
- Response contains `messages[0].total` so the agent knows when to stop paginating.
- Agent fetches everything for the window, keyword-filters client-side. There is no server-side keyword filter.

**Per-record URL pattern (for the digest's links):**
```
https://www.biorxiv.org/content/{doi}v{version}
```

**Subject categories** (the API returns `category` per record): can be used as a secondary signal during clustering, but never as a primary filter. The watchlist keywords are the gate.

---

## medRxiv

Same operator as bioRxiv, same API, same response shape. Only the path segment changes.

**Endpoint (date window):**
```
https://api.biorxiv.org/details/medrxiv/{YYYY-MM-DD}/{YYYY-MM-DD}/{cursor}
```

**Per-record URL pattern:**
```
https://www.medrxiv.org/content/{doi}v{version}
```

The `fetch-preprint-recent` skill takes `server` as a parameter and handles both. No need for separate code paths.

---

## PubMed

Two transports — prefer the MCP if available, fall back to E-utilities.

### MCP (preferred when connected)

If a PubMed MCP server is configured (the runtime exposes tools matching `mcp__*PubMed*__search_articles` and `mcp__*PubMed*__get_article_metadata`), use it. Pass the date-bounded query as a single string to `search_articles`; pull metadata with `get_article_metadata`.

### E-utilities (fallback, always works)

```
Search:   https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&term={query}&retmode=json&retmax=200
Summary:  https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=pubmed&id={pmids_csv}&retmode=json
Abstract: https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=pubmed&id={pmids_csv}&rettype=abstract&retmode=xml
```

Optional API key via `&api_key=...` (3 → 10 rps). Look up `NCBI_API_KEY` in env; if absent, just go slower.

### Query template

```
( "kw1"[Title/Abstract] OR "kw2"[Title/Abstract] OR ... )
AND ("YYYY/MM/DD"[PDAT] : "YYYY/MM/DD"[PDAT])
```

- Use `[Title/Abstract]` to disable PubMed's automatic-term-mapping (which would silently expand keywords to MeSH trees).
- `PDAT` (publication date) is the default. Use `EDAT` (entry date) only when the user wants "newly indexed even if old."
- One AND-combined date filter. Never two date filters — they intersect to nothing if mistyped.

**Per-record URL pattern:**
```
https://pubmed.ncbi.nlm.nih.gov/{pmid}/
```

DOI URL (publisher's page) as secondary link if `doi` is present in the record.

---

## Cross-source dedupe rules

A bioRxiv preprint and its PubMed published version are *the same paper*. Dedupe before relevance filtering and clustering — otherwise the relevance filter will treat them as separate papers and double-count, breaking novelty scoring.

**Dedupe order of operations:**

1. Match by DOI when both records carry one. PubMed records often carry the publisher DOI; preprint records carry the bioRxiv DOI (`10.1101/...`). Same paper can have both — use whichever overlaps.
2. If no shared DOI, match by normalized title (lowercase, strip punctuation, collapse whitespace) + first author surname. Levenshtein ratio > 0.92 on the title is a strong signal.
3. When a duplicate is detected, **prefer the PubMed record as the primary entry** but keep the preprint URL as a secondary `preprint_version` link in the merged record.

If unsure, do not merge — flag for REVIEW. Two real but coincidentally similar papers exist; better to surface both than to silently lose one.

---

## What's not in this registry (and why)

- **arXiv q-bio**: deliberately excluded in v1. Most cs/q-bio of interest gets cross-posted to bioRxiv. Add later if needed.
- **chemRxiv, ChemRxiv, Research Square, etc.**: out of v1 scope. Easy to add — they have similar APIs — but they widen the noise floor without a clear gain on the current watchlist.
- **Journal-specific feeds (Nature, Science, Cell)**: PubMed indexes them; no reason to fetch them separately.
- **Google Scholar**: no API, scraping is brittle and against ToS. Skip.

---

## Failure modes and what to do

| Failure                                    | What it means                                           | Agent's response                                  |
| ------------------------------------------ | ------------------------------------------------------- | ------------------------------------------------- |
| bioRxiv API returns 5xx                    | Their service is down (happens occasionally)            | Retry once with backoff; on second fail, log and proceed with other sources |
| medRxiv same                               | Same                                                    | Same                                              |
| PubMed esearch returns 0 results           | Either the query is wrong or genuinely nothing this week | Verify query string; if correct, mark as thin source |
| PubMed efetch (abstract) times out         | Common with batches > 100                               | Halve batch and retry; record null abstracts after second fail |
| All three fail                             | Network problem on the local machine                     | Halt the run; report to the user; do not write a digest |
| Single source returns thousands of records  | Watchlist is too broad for that source                   | Apply stricter relevance threshold; surface "watchlist may be over-broad" warning in digest |
