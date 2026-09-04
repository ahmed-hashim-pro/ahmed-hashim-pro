## Ahmed Hashim

Software architect, 11 years. I design systems where a language model is a
component with a contract — inputs it has to validate, outputs it has to
justify, and things it is not allowed to do.

Most of my recent work sits on the awkward parts of that: proving an answer came
from somewhere, telling a real regression apart from a model having an off day,
and deciding what an agent may do without asking a human first.

---

### Projects

#### [noisefloor](https://github.com/ahmed-hashim-pro/noisefloor) — a regression harness for systems that don't give the same answer twice

Most eval tooling answers *"what score does this get?"* The question that blocks
a merge is *"did this change make it worse?"* — and that is unanswerable on a
non-deterministic system until you know how much it moves on its own.
`noisefloor` runs the target N times, measures the spread, and only calls
something a regression when the delta clears the noise. It ships a measured
noise profile of a real RAG agent, which is also how it found a false positive
in itself.

`Python` · 202 tests · quickstart runs with no API key, no network

#### [sqlguard-mcp](https://github.com/ahmed-hashim-pro/sqlguard-mcp) — let an agent query a real database without giving it write access

Reads run immediately under a row cap and a timeout. Writes are refused until a
human approves that exact statement, in a separate process the agent has no way
to reach — the approval is bound to a statement rather than a capability, and is
single-use through an atomic filesystem operation rather than a mutex, because
the server and the approving CLI are different programs. The classifier refuses
what it cannot prove is a read, which is what catches a `DELETE` hidden inside a
CTE that opens with `WITH`.

`Go` · `MCP` · 127 tests · end-to-end suite drives the real binary over stdio

#### [rag-knowledge-agent](https://github.com/ahmed-hashim-pro/rag-knowledge-agent) — a CLI RAG agent that shows its work

Hybrid retrieval — dense vectors and BM25, fused by reciprocal rank — with every
claim cited as `[source:heading]` and a confidence gate that declines instead of
guessing when the corpus does not support an answer. Retrieved text is handled
as data and never as instructions, so injection resistance is a property of the
design rather than a filter bolted on. Indexing runs entirely locally, so it
costs nothing and needs no key.

`Python` · `ChromaDB` · `Claude` · 109 tests, model stubbed throughout

#### [local-network-mcp](https://github.com/ahmed-hashim-pro/local-network-mcp) — an MCP server with a real deny boundary

Lets an agent discover, ping, inspect and SSH into devices on a local network.
The three tools that can change state — arbitrary local shell, arbitrary remote
shell, kill by PID — are denied unless explicitly enabled, and the switch lives
in the server's environment where a tool argument cannot reach it. An LLM
decides when tools run, so the model must not be able to grant itself a
capability.

`Python` · `MCP` · 62 tests that assert the refusal, not the execution

---

### My Stream — closed source

A multi-model AI publishing platform I build and run. Angular/Ionic on AWS,
routing across seven LLM providers behind a single interface with per-model
quality calibration, so a cheaper or weaker model degrades predictably instead
of failing in surprising ways.

---

### Stack

| | |
| --- | --- |
| **Working with models** | Anthropic / Claude, MCP, RAG, hybrid retrieval, evals, multi-provider routing |
| **Languages** | Go, Python, TypeScript, C++ |
| **Web & mobile** | Angular, Ionic, Node |
| **Infrastructure** | AWS, Docker, GitHub Actions |

---

[geohashim.com](https://geohashim.com) · Medo Apps
