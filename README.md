# Prathamesh Kalamkar

**Trustworthy AI for software engineering · software security · reliable agent systems**

I am a software engineer in Dublin building and studying AI systems that modify code or take external actions. My work asks a practical research question: **what evidence is strong enough to trust an agent's output?** I answer it with executable ground truth, failure-oriented experiments, explicit uncertainty, and reproducible artifacts.

[Research portfolio](https://prathamesh-git9.github.io/portfolio-website/) · [LinkedIn](https://www.linkedin.com/in/prathamesh-kalamkar/) · [Email](mailto:prathemesh7744@gmail.com)

## Research artifacts

### [Security Oracle Discrimination Audit](https://github.com/prathamesh-git9/security-oracle-discrimination)

An execution-grounded audit of whether security checkers respond to program behaviour or merely to surface form.

- **Controlled study:** 5 oracles × 96 Python implementations across 8 weakness classes; all labels earned by running exploit witnesses.
- **Production study:** 140 real CVE fixes from 65 projects. The evaluated tools produced unchanged verdicts across **92.9%–98.6%** of fixes.
- **Cross-study result:** synthetic and production detection rates correlate at **Spearman ρ = 0.782**.
- Reproducible CLI, fixed protocol, raw results, bootstrap intervals, production manifest, and green CI.

Status: **public research artifact and manuscript; not peer-reviewed**.

### [Secure Instruction Placement](https://github.com/prathamesh-git9/secure-instruction-placement)

A controlled study of whether identical secure-coding guidance works differently in task prompts, repository instructions, both, or neither. The repository separates pilot tasks from a protected holdout, records a deterministic run schedule, and pre-specifies task-clustered analysis.

Status: **work in progress; pilot evidence is non-confirmatory**.

## Selected systems

| Project | Problem | Evidence |
| --- | --- | --- |
| [PatchPilot](https://github.com/prathamesh-git9/patchpilot) | Provider-authored OpenAPI changes should migrate affected customer code instead of becoming unread changelog entries. Built in response to YC's [Self-Maintaining APIs](https://www.ycombinator.com/rfs) request. | Deterministic JS/TS/Python patches, signed migration manifests, GitHub App delivery, crash/replay handling, 12 releases, green CI. |
| [Effect Broker](https://github.com/prathamesh-git9/effect-broker) | A timed-out agent action may have committed even when its acknowledgement was lost. | Stable idempotency contracts, authoritative reconciliation, `outcome_unknown`, and a process-kill crash matrix on SQLite and PostgreSQL. |
| [Agent Redteam](https://github.com/prathamesh-git9/agent-redteam) | Agent-security claims need outcome evidence, not subjective transcript review. | Executable attack oracles, clean-twin counterfactual replay, guardrail-effectiveness measurement, SARIF, and regression baselines. |
| [Agentic Digital Twin](https://github.com/prathamesh-git9/agentic-digital-twin) | A public AI profile must not turn web search or model fluency into invented personal claims. | Source-grounded answers, a pre-prompt authority gate, measured retrieval and claim verification, and 191 offline tests. |

## Design principles

- **Earn labels through execution.** If a claim can be checked by running an exploit, crash, or contract test, run it.
- **Model ambiguity explicitly.** `UNKNOWN` is a valid result; silence or timeout is not evidence of safety.
- **Make authority structural.** External effects cross explicit, recorded approval boundaries.
- **Publish the audit trail.** Protocols, raw records, limitations, hashes, and negative results belong beside the code.
- **Keep claims narrower than evidence.** Artifacts are not publications, pilots are not confirmatory studies, and passing tests are not user adoption.

## Background and current direction

I hold an MSc in Cybersecurity from Dublin Business School (2025) and a bachelor's degree in Computer Science from Savitribai Phule Pune University (2024). I am preparing for PhD applications focused on trustworthy AI for software engineering, especially evaluation integrity, secure code generation, and dependable agent actions.

I welcome technically specific feedback, independent reproductions, and research collaboration. The best starting point is the [oracle audit](https://github.com/prathamesh-git9/security-oracle-discrimination) or an email to [prathemesh7744@gmail.com](mailto:prathemesh7744@gmail.com).
