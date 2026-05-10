# Prompts

A single paste-and-go kickoff prompt that hands a Claude Code session over to the project's orchestrator agent (`papersynthesis-orchestrator`). The orchestrator handles every other intent in plain English from your follow-up message.

## How to use

1. Make sure you've installed `papersynthesis-orchestrator` to `~/.claude/agents/` (see Step 4 of the project's `README.md`).
2. Open Claude Code from inside the project root so the working directory matches:
   ```
   cd path/to/papersynthesis
   claude
   ```
3. Paste the contents of [`kickoff.md`](kickoff.md) as your first message. Or reference it with `@prompts/kickoff.md` if your Claude Code session supports `@`-references.
4. The orchestrator will load project context and pause, waiting for you to describe what you want.
5. Say what you want, in plain English:
   - "Run the weekly paper digest." → WEEKLY intent
   - "Catch me up on the last 3 weeks." → CATCH_UP intent
   - "What's new on diffusion models in the last 14 days?" → ON_DEMAND intent
   - "Re-run last week from cache. I just edited the relevance criteria." → RE_SYNTHESIZE intent
   - "Deep-read the Smith et al. paper from week 19." → DEEP_READ intent

The orchestrator detects the intent, fans out the right subagents (search → extract → synthesize), and surfaces a combined report when done.

## Why only one prompt

Earlier versions of this project shipped intent-specific prompts (`weekly.md`, `catchup.md`, etc.) that each invoked a worker agent directly with explicit framing. With the project-level orchestrator agent, that explicit framing happens inside the orchestrator's intent-detection logic — written into `orchestrator.md` once, applied at runtime. The prompts collapsed to one.

## Editing this prompt

If you find yourself rewriting the same context every session, fold the addition into `kickoff.md`. Anything that belongs as durable project context goes in `orchestrator.md` or `shared-context/` instead — both are read by the orchestrator at startup.
