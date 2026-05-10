# Prompts

Pre-written kickoff prompts you can paste at the start of a Claude session (or reference with `@`) to invoke the `literature-scan-coach` agent for a specific intent.

Each prompt sets enough project context that the coach can route to the right workflow without further clarification, then explicitly asks Claude to invoke the coach.

## How to use

Open Claude Code in this project folder so the working directory is correct:

```
cd /Users/kushaldsouza/Documents/Thinking/papersynthesis
claude
```

Then either:
- Paste the contents of the relevant prompt file as your first message, or
- Reference it with `@prompts/<file>.md` if your Claude Code session supports `@`-references.

If you're not sure which prompt to use, start with `kickoff.md` — it gives the coach enough context to detect intent from a follow-up message.

## Available prompts

| File | When to use |
|---|---|
| [`kickoff.md`](kickoff.md) | Generic entry. Sets project context and lets the coach decide what to run from your follow-up. |
| [`weekly.md`](weekly.md) | Standard Monday-morning weekly digest. The 90% case. |
| [`catchup.md`](catchup.md) | You missed weeks and want to back-fill — fill in N before pasting. |
| [`on-demand.md`](on-demand.md) | Thematic question outside the regular cadence — fill in topic and window. |
| [`re-synthesize.md`](re-synthesize.md) | Re-render an existing digest from cached fetches after editing relevance-criteria.md or synthesis-style.md. |

## Editing these prompts

Treat them as templates you tune over time. If you find yourself rewriting the same context every week, fold the addition into `kickoff.md` so future sessions inherit it. The coach reads `orchestrator.md` and `shared-context/` at startup, so anything that belongs as durable project context should go in one of those files instead of in a prompt.
