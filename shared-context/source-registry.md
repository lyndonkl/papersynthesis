# Source Registry

Endpoints, query templates, and operational notes for the four sources the paper-synthesizer agent reads each week (bioRxiv, medRxiv, PubMed, arXiv). This file is read by the agent during the run; you only edit it if a source's API actually changes or you want to change which arXiv categories get queried.

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

The same paper can appear on multiple sources: a bioRxiv preprint can have a PubMed published version, an arXiv paper can be cross-listed on bioRxiv, and an arXiv paper can have a PubMed publication once it lands in a journal. Dedupe before relevance filtering and clustering — otherwise the relevance filter will treat them as separate papers and double-count, breaking novelty scoring.

**Dedupe order of operations:**

1. Match by DOI when both records carry one. PubMed records often carry the publisher DOI; bioRxiv / medRxiv records carry the `10.1101/...` DOI; arXiv records sometimes carry a publisher DOI once published. Same paper can have multiple DOIs over its life — use whichever overlaps.
2. If no shared DOI, match by normalized title (lowercase, strip punctuation, collapse whitespace) + first author surname. Levenshtein ratio > 0.92 on the title is a strong signal.
3. When a duplicate is detected, **preference order: PubMed (published) > bioRxiv / medRxiv (life-sciences preprint with DOI) > arXiv (CS preprint)**. Keep the alternate URLs as `also: {server} version` links in the merged record so the operator can drill into either the preprint or the published version.

If unsure, do not merge — flag for REVIEW. Two real but coincidentally similar papers exist; better to surface both than to silently lose one.

---

## arXiv

Atom-XML API. Different shape from the others — datetime-range query syntax, hard rate limit, distinct category taxonomy.

**Endpoint:**
```
http://export.arxiv.org/api/query?search_query={URL_ENCODED_QUERY}&sortBy=submittedDate&sortOrder=descending&start={offset}&max_results=200
```

**Auth:** none. **Rate limit:** 1 request per 3 seconds (sleep between paginated requests). **Page size:** 200 max.

### Query template

```
submittedDate:[YYYYMMDDHHMM TO YYYYMMDDHHMM]
  AND (cat:cs.LG OR cat:cs.CL OR cat:stat.ML)             # optional category clause
  AND (all:"keyword phrase" OR all:singleword OR ...)
```

Use `from + 0000` and `to + 2359` so the window is fully inclusive. Sort descending so pagination can bail out as soon as result dates fall before `from`. The `all:` field searches title + abstract + authors.

### arXiv categories I want queried (operator-owned)

The default category set this project uses is **CS / ML focused**:

```
cs.LG    # Machine Learning
cs.CL    # Computation and Language
cs.CV    # Computer Vision
cs.AI    # Artificial Intelligence
cs.NE    # Neural and Evolutionary Computing
stat.ML  # Statistics: Machine Learning
```

Reasonable additions if your watchlist drifts:

- **Quantitative biology (cross-disciplinary):** `q-bio.QM, q-bio.GN, q-bio.MN, q-bio.NC` — adds CS-leaning biology that may not be on bioRxiv.
- **Math / stats:** `math.ST, math.PR, math.OC, stat.ME, stat.AP`
- **Physics-adjacent:** `physics.data-an, cond-mat.stat-mech`

To search **all of arXiv** (no category restriction), pass `categories=null` to `fetch-arxiv-recent`. Useful only when the keyword filter is very tight; otherwise the noise floor swamps the digest.

### Per-record URL pattern

```
https://arxiv.org/abs/{id}        # abstract page (preferred for digest links)
https://arxiv.org/pdf/{id}.pdf    # PDF (optional secondary link)
```

The canonical ID is the paper number with no version suffix — `2605.12345` for post-2007 papers, `cs.LG/0301001` for legacy. Strip `vN` from the URL when computing the canonical ID for dedupe.

---

## Failure modes and what to do

| Failure                                    | What it means                                           | Agent's response                                  |
| ------------------------------------------ | ------------------------------------------------------- | ------------------------------------------------- |
| bioRxiv API returns 5xx                    | Their service is down (happens occasionally)            | Retry once with backoff; on second fail, log and proceed with other sources |
| medRxiv same                               | Same                                                    | Same                                              |
| PubMed esearch returns 0 results           | Either the query is wrong or genuinely nothing this week | Verify query string; if correct, mark as thin source |
| PubMed efetch (abstract) times out         | Common with batches > 100                               | Halve batch and retry; record null abstracts after second fail |
| arXiv 429 rate-limit response              | Pagination too aggressive (need 3-second sleep)          | Sleep 5 seconds, retry; if it persists, halve `max_results` and continue |
| arXiv Atom XML parse fails                 | Malformed feed page                                       | Retry once with 5-second backoff; on second fail, log and skip the page |
| All four sources fail                      | Network problem on the local machine                     | Halt the run; report to the user; do not write a digest |
| 1-2 sources fail, the others returned      | Partial coverage                                          | Proceed; surface the partial coverage prominently in the digest's "Notes for next week" line |
| Single source returns thousands of records  | Watchlist (or arXiv categories) too broad for that source | Apply stricter relevance threshold; surface "watchlist may be over-broad" warning in digest |
