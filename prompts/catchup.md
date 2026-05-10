# Catch-up prompt

Use this when you've missed weeks and want to back-fill. Fill in `N` (the number of weeks to catch up on) before pasting.

---

I'm working in my literature-scan project. Working directory is the project root.

I missed the last **N = ___** weeks. Run a catch-up.

Invoke the `literature-scan-coach` agent with intent CATCH_UP. It should:

1. Run its pre-flight check.
2. Compute N week windows. Run them **oldest first** so each successive run can read the earlier digests as historical context (this is non-negotiable — running newest-first breaks the continuity tagging).
3. For each week, spawn the `paper-synthesizer` subagent with that week's window and tag, and **wait for it to finish** before spawning the next week's run.
4. If a week's run fails (e.g., all four sources down), halt the catch-up at that point, report the failure, and let me decide whether to retry or skip.
5. After all N runs, give me a single combined summary: each week's digest path, kept count, and one-line headline, plus any cross-week continuity flags.

Do not collapse weeks — I need to see each headline separately.
