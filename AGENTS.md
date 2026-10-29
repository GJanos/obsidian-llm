# obsidian-llm (LAIWM)

Local AI Workflow Manager: a locally running LLM pipeline that runs workflows against the user's
Personal Obsidian vault, with **no data ever leaving the machine** (the whole reason it exists).
Two workflows: `monthly_summary` (multi-pass condense → synthesize over a month of daily notes) and
`semantic_search`. `README.md` covers the hardware, setup and both workflows; `docs/` the rest.

## Rules

- Python 3.12 with `uv`, run **in WSL2** (Windows CPython is blocked on this machine); Ollama with
  IPEX-LLM serves `qwen3:14b` and `nomic-embed-text` on the Intel Arc iGPU from the Windows side.
  `uv run manager.py --prompt "…" [--debug]`.
- **Don't read `output/`** (git-ignored): its summaries are made from daily notes, which are
  fenced for agents. The pipeline reads them locally; an agent must not.

## Map

<!-- map:start -->
| Path | What | Go here when |
|---|---|---|
| `workflows/` | `monthly_summary.py` and `semantic_search.py`, one module per workflow | changing what a workflow does |
| `docs/` | `docs/modes.md`, `docs/technologies.md`, `docs/user.md`, `docs/devlog.md` | the design choices, the stack, the history |
<!-- map:end -->

The entry point and helpers sit at the root: `manager.py` (CLI, routes a prompt to a workflow),
`classifier.py` (picks the workflow), `config.py` (models, paths, Ollama), `embeddings.py`,
`utils.py`.
