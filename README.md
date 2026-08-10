I build agent infrastructure — the correctness and recovery layer underneath tool-calling AI systems.

A more capable model does not fix idempotency, determinism, crash recovery, authority boundaries, or honest uncertainty. Those are information and atomicity problems, not reasoning ones. When a tool call times out, the local journal cannot distinguish *the request never arrived* from *the request committed and the acknowledgement was lost* — no amount of intelligence recovers that bit. So the work below shares one design signature: when the truth is not knowable, the system records an explicit unknown and stops at a human gate instead of guessing well.

### Research: trustworthy AI for software engineering

- **[secure-instruction-placement](https://github.com/prathamesh-git9/secure-instruction-placement)** - A reproducible study of whether placing identical secure-coding guidance in a task, repository context, both, or neither changes AI coding-agent outcomes. The public artifact includes a versioned protocol, literature/novelty log, validated 11-task subset across six weakness families, benchmark-audit tools, provenance-recording runner, 29 tests with CI, and a four-condition pilot release with generated sources, machine-readable records, hashes, and executable functional/security outcomes. Status is stated precisely: the pilot is non-confirmatory and no placement effect is claimed yet.

### Selected work

**Correctness under retries and crashes**

- **[effect-broker](https://github.com/prathamesh-git9/effect-broker)** — A correctness boundary for side-effecting agent tools: one downstream idempotency key across every retry, authoritative reconciliation, and an honest `outcome_unknown` instead of a fake exactly-once guarantee.
- **[agent-runtime](https://github.com/prathamesh-git9/agent-runtime)** — Durable, resumable execution for tool-calling loops. An event-sourced journal and deterministic replay make crash recovery something that never re-fires a side effect.
- **[effect-browser](https://github.com/prathamesh-git9/effect-browser)** — Crash-safe control plane for AI-driven browser operations. Navigation runs freely; external commits require exact action-bound authority.
- **[promise-ledger](https://github.com/prathamesh-git9/promise-ledger)** — Versioned, evidence-backed system of record for commitments. Models propose with sources, humans activate, supersession is explicit rather than inferred.

**Serving and coordination**

- **[llm-gateway](https://github.com/prathamesh-git9/llm-gateway)** — Self-hostable OpenAI-compatible inference gateway: policy routing with fallback chains, circuit breakers, semantic caching, hard per-tenant budgets, Prometheus metrics.
- **[agent-mesh](https://github.com/prathamesh-git9/agent-mesh)** — Event-driven multi-agent backend: consumer groups, at-least-once delivery with idempotency, dead-letter recovery, and fan-in that degrades on partial failure instead of hanging.
- **[answer-engine](https://github.com/prathamesh-git9/answer-engine)** — Production RAG and tool-calling backend. Adaptive retrieval routing, hybrid BM25 + vector fused with RRF, and grounding verification that reports whether the answer is actually supported by its citations.
- **[mcp-servers](https://github.com/prathamesh-git9/mcp-servers)** — Six independently runnable MCP servers on the 2.0 SDK: grounded CV, repo intelligence, web research, ATS jobs, outcome ledger, coding workflows. Typed inputs and outputs, per-server limits, and a socket-restricted test suite so nothing quietly reaches the network.

**Grounding and evaluation**

- **[digital-twin](https://github.com/prathamesh-git9/digital-twin)** — A source-grounded twin that answers only from a structured CV corpus and live repo metadata, behind an authority gate: background research can *propose* visitor context, but no code path admits it until the visitor confirms. Retrieval measured, not asserted — recall@8 12/24 → 24/24, and a claim-verification pass took precision 0.556 → 0.941 by deleting unsupported claims rather than softening them.

**Assurance**

- **[agent-redteam](https://github.com/prathamesh-git9/agent-redteam)** — Adversarial testing and runtime guardrails for LLM agents. A layered oracle scores attack success from planted evidence rather than eyeballing model output, and rolls it into CVSS-style risk you can gate CI on.
- **[reachable](https://github.com/prathamesh-git9/reachable)** — CVE triage by static call-graph reachability, emitting OpenVEX. Three verdicts, never two: uncertainty degrades to `UNKNOWN`, never to not-reachable.
- **[trustdesk](https://github.com/prathamesh-git9/trustdesk)** — Grounded drafting for vendor security questionnaires: hybrid retrieval behind a calibrated relevance floor, mandatory human review, append-only audit trail.

### How I build

- **Prove the failure, not the happy path.** `effect-broker` ships a crash matrix that kills a worker with a real `os._exit(137)` after the target commits but before the receipt is written — the exact window that causes double-charges — then asserts the *target-side* effect count after recovery.
- **Durable before dispatch.** Append the intent to a journal, then act. Recovery reads the log, never process memory, and compare-and-swap transitions keep two workers from advancing the same record.
- **Degrade to unknown, not to a guess.** Every one of these systems has a verdict for *cannot be determined*, and it is never the optimistic one.
- **Keep a human on the authority boundary.** Irreversible or external effects pass through an explicit gate with recorded scope, not a confidence threshold.
- **Default to offline and deterministic.** Test suites and demos run with no API keys, so what is under test is the system's behaviour rather than the provider's mood.
- **Ship it like a service.** Typed Python 3.11+, FastAPI / CLI / MCP surfaces, Docker Compose, migrations where there is schema, and CI green across a Python version matrix on every repo above. All MIT.

### Elsewhere

Dublin, Ireland · [prathemesh8459@gmail.com](mailto:prathemesh8459@gmail.com) · [@pkalamkar_](https://x.com/pkalamkar_)
