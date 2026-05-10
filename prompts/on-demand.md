# On-demand thematic prompt

Use this for an off-cadence thematic question — "what's new on X in the last N weeks." Fill in topic and window before pasting.

---

I'm working in my literature-scan project. Working directory is the project root.

I have a thematic question, not a calendar question:

- **Topic:** ___
- **Window:** last ___ days (default 14 if I leave this blank)

Invoke the `literature-scan-coach` agent with intent ON_DEMAND. It should:

1. Run its pre-flight check.
2. Check whether the topic above is already covered by my `shared-context/watchlist.md`:
   - If yes, pass the watchlist as-is — the keyword filter will hit.
   - If no, write a one-shot per-week override at `ops/paper-synthesizer/overrides/{YYYY-WW}-ondemand.md` adding the topic as a single keyword, with a note that this is an on-demand thematic run.
3. Spawn the `paper-synthesizer` subagent with explicit framing: on-demand thematic digest (not a regular weekly digest), do not append to the README's "Recent digests" list, use the topic and window I gave above.
4. When the subagent returns, give me the digest path, kept / dropped counts, the 30,000-ft preview, and a suggestion (advisory only — do not edit) on whether the topic should be promoted to my persistent watchlist.
