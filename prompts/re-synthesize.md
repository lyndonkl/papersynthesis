# Re-synthesize prompt

Use this after editing `shared-context/relevance-criteria.md` or `shared-context/synthesis-style.md` — re-renders an existing weekly digest from cached fetch results, without paying for fresh network fetches.

---

I'm working in my literature-scan project. Working directory is the project root.

I just edited `shared-context/relevance-criteria.md` and / or `shared-context/synthesis-style.md`. Re-synthesize an existing weekly digest from cache so I can see what my edits changed.

- **Week to re-synthesize:** ___ (default: the most recent digest in `ops/paper-synthesizer/`)

Invoke the `literature-scan-coach` agent with intent RE_SYNTHESIZE. It should:

1. Run its pre-flight check.
2. Confirm `ops/paper-synthesizer/.cache/{YYYY-WW}-biorxiv.json`, `-medrxiv.json`, `-pubmed.json`, and `-arxiv.json` all exist for the target week. If any cache file is missing, ask whether to refetch that source or skip it.
3. Spawn the `paper-synthesizer` subagent with explicit framing: re-synthesize from cache, skip pipeline Steps 3-5b (no fresh fetches), load the cached records, run filter + cluster + synthesis only.
4. Overwrite the existing digest.
5. When the subagent returns, give me a one-line **diff vs prior version**: change in kept / dropped counts, and whether any clusters were renamed. This is the whole point of the re-run — I need to see the impact of my criteria edit.
