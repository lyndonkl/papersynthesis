# Weekly digest prompt

Paste this on Monday morning (or whenever you want the standard weekly digest). The coach computes the window automatically — today minus 7 days through yesterday, inclusive.

---

I'm working in my literature-scan project. Working directory is the project root.

Run the regular weekly paper digest.

Invoke the `literature-scan-coach` agent. It should:

1. Run its pre-flight check (confirm `orchestrator.md`, `shared-context/watchlist.md`, `shared-context/source-registry.md`, `ops/paper-synthesizer/` are all visible).
2. Detect intent as WEEKLY.
3. Compute the window: today minus 7 days through yesterday, inclusive. ISO week tag accordingly.
4. Check `ops/paper-synthesizer/` for an existing digest at this week's tag — if present, ask before overwriting.
5. Spawn the `paper-synthesizer` subagent with the explicit weekly-run parameters.
6. When the subagent returns, give me the digest path, kept / dropped counts, the 30,000-ft preview paragraph verbatim, and any warnings.

If any source fails to return results, surface it but proceed with the others — only halt if all four fail.
