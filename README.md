## Ahmed Hashim

Software architect, 11 years. I came to software from geology, which is
probably why I like systems where being approximately right is not good enough
— storage engines, flight control, and lately what a language model is allowed
to do.

Most of my recent work sits on two questions that turn out to be the same
question: **what is this system permitted to do, and how would I know if it
stopped working?**

---

### Open source

#### [atlas-graph-db](https://github.com/ahmed-hashim-pro/atlas-graph-db) — a graph database written from scratch

Storage engine with write-ahead logging, snapshots and crash recovery;
transactions, property/unique/fulltext indexes, traversals and graph algorithms;
a full AQL query language over the top; a multi-user Fastify server with
argon2id auth, revocable sessions, API tokens and a permission matrix; a typed
isomorphic client SDK; and the Knowledge Graph Explorer web app. Durability came
before features — a graph store that loses a write on power failure is a cache
with extra steps — so recovery was tested by killing the process mid-transaction
before anything was built on top of it.

`TypeScript` · `Angular` · 468 tests · benchmark gate at 1M nodes / 5M edges, signed off in `docs/BENCHMARKS.md`

#### [sqlguard-mcp](https://github.com/ahmed-hashim-pro/sqlguard-mcp) — let an agent query a real database without giving it write access

Reads run under a row cap and a timeout. Writes are refused until a human
approves that exact statement, in a separate process the agent cannot reach —
the approval is bound to a statement rather than a capability, and is single-use
through an atomic filesystem operation rather than a mutex, because the server
and the approving CLI are different programs. Deployed to Kubernetes, approving
becomes `kubectl exec`, so the boundary needs cluster credentials rather than
access to a file.

`Go` · `MCP` · `Kubernetes` · `Helm` · 138 tests · CI stands up a real cluster and drives the deployed service

#### [llm-contract-router](https://github.com/ahmed-hashim-pro/llm-contract-router) — fall back to a cheaper model without breaking the caller

Routes across providers behind one interface, adapting each request to the
target model's tier — a compact model gets the schema restated, an example to
copy and temperature zero; a frontier model gets none of that, because the
scaffolding crowds out the task. The answer is validated against your schema,
and a failure sends the model the specific constraints it broke. Degraded means
cheaper and slower, never malformed.

`TypeScript` · zero runtime dependencies · 105 tests, no API keys

#### [noisefloor](https://github.com/ahmed-hashim-pro/noisefloor) — a regression harness for systems that don't give the same answer twice

Eval tooling answers *"what score does this get?"* The question that blocks a
merge is *"did this change make it worse?"* — unanswerable on a
non-deterministic system until you know how much it moves on its own. Runs the
target N times, measures the spread, and only calls something a regression when
the delta clears it. Capturing a real baseline found a false positive in
noisefloor itself.

`Python` · 202 tests · quickstart runs with no API key and no network

#### [rag-knowledge-agent](https://github.com/ahmed-hashim-pro/rag-knowledge-agent) — a CLI RAG agent that shows its work

Hybrid retrieval — dense vectors and BM25, fused by reciprocal rank — with every
claim cited as `[source:heading]` and a confidence gate that declines rather
than guessing. Retrieved text is handled as data and never as instructions, so
injection resistance is a property of the design rather than a filter.

`Python` · `ChromaDB` · `Claude` · 109 tests, model stubbed throughout

#### [local-network-mcp](https://github.com/ahmed-hashim-pro/local-network-mcp) — an MCP server with a real deny boundary

Lets an agent discover, ping, inspect and SSH into devices on a local network.
The three tools that change state are denied unless explicitly enabled, and the
switch lives in the server's environment where a tool argument cannot reach it.

`Python` · `MCP` · 62 tests that assert the refusal, not the execution

---

### Closed source

The rest of the last decade.

**My Stream** — a multi-model AI publishing platform I build and run.
Angular/Ionic and Android on AWS, routing across seven LLM providers behind one
interface with per-model quality calibration, so a cheaper model degrades
predictably instead of failing in surprising ways.

**Drone autonomy (HEAR / droneLeaf)** — C++ onboard software for unmanned
aircraft: mission-scenario control, an onboard REST API and websocket link,
machine identity, and a ROS/CMake cross-compilation toolchain for getting it
onto the target hardware.

---

### Stack

| | |
| --- | --- |
| **Languages** | TypeScript, Python, Go, C++, Java |
| **Working with models** | Anthropic / Claude, MCP, RAG, hybrid retrieval, evals, multi-provider routing |
| **Systems** | Storage engines, query languages, distributed services, real-time C++/ROS |
| **Web & mobile** | Angular, Ionic, Node, Android |
| **Infrastructure** | AWS, Docker, Kubernetes, Helm, GitHub Actions |

---

[geohashim.com](https://geohashim.com) · Medo Apps
