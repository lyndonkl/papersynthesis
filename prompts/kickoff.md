Read `orchestrator.md` (in the project root) and follow that contract for this session — **you ARE the orchestrator**.

Do **not** spawn yourself as a subagent via the Agent tool. The Claude Code harness strips the `Agent` (spawn) tool from any agent that is itself running as a subagent, so spawning the orchestrator that way leaves it unable to fan out the search / extract / synthesize lanes — the entire pipeline collapses to single-context execution and the contract's verification gates and per-paper context isolation are both defeated.

Run the contract directly from this main conversation, where you have the full toolset (`Agent`, `AskUserQuestion`, `Glob`, `Read`, `Write`, `Bash`, `WebSearch`, `WebFetch`). Honour every section: Gathering operator intent → Query expansion → Pre-flight check → Parallelism rules (multi-call messages for every fan-out stage) → the streaming pipeline → verification gates → report-back.

The context for this run — anything I've said in the message before / alongside / after this one about topic, time window, and digest shape — is the operator input the contract expects you to gather. If anything is missing or ambiguous, use `AskUserQuestion` once (batched) before proceeding.
