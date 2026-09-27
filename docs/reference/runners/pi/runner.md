Below is a concrete implementation spec for the **Pi (pi-coding-agent CLI)** runner shipped in Untether (v0.5.0).

---

## Scope

### Goal

Provide the **`pi`** engine backend so Untether can:

* Run Pi non-interactively via the **pi CLI** (`pi --print`).
* Stream progress by parsing **`--mode json`** (newline-delimited JSON). Each line is a JSON object.
* Support resumable sessions via **`--session <token>`** (Untether emits a canonical resume line the user can reply with).

### Non-goals (v1)

* Interactive TUI flows (session picker, prompts, etc.)
* RPC mode (requires a long-running process and JSON commands)

---

## UX and behavior

### Engine selection

* Default: `untether` (auto-router uses `default_engine` from config)
* Override: `untether pi`

### Resume UX (canonical line)

Untether appends a **single backticked** resume line at the end of the message, like: