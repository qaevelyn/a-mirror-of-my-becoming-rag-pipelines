# A Mirror of My Becoming™ — RAG Pipelines

**Five retrieval-augmented generation pipelines. One MacBook Air. No cloud.**

Five working RAG pipelines built on consumer hardware with no cloud dependency, no vendor API, and no team. Each ship is a separate repository. This repository is the index.

Every pipeline reads documents from disk, chunks them, embeds them locally via Ollama, and writes them to a local Chroma vector store. **Nothing leaves the machine.** See [SETUP.md](SETUP.md) for how to point any ship at your own corpus.

---

## The five ships

| # | Ship | Platform | Type |
|---|------|----------|------|
| 1 | **DeepSeek RAG** | DeepSeek, local via Ollama | Standard RAG |
| 2 | **IBM Granite Agentic RAG** | IBM Granite, local | Agentic RAG |
| 3 | **IBM Granite RAG** | IBM Granite, local | Standard RAG, cross-platform |
| 4 | **IBM Granite Agentic RAG** | IBM Granite, local | Agentic, cross-platform |
| 5 | **IBM Granite Agentic RAG + EvidenceFlow** | IBM Granite, local | Evidence-verified, fail-closed |

**Ship 1** — DeepSeek RAG (standard). Built in a Jupyter notebook, originally on AWS SageMaker, lost with the instance, rebuilt locally from the author's archive. The rebuild was cleaner than the original.
**Repo:** [a-mirror-of-my-becoming-rag-ship1-deepseek](https://github.com/qaevelyn/a-mirror-of-my-becoming-rag-ship1-deepseek)

**Ship 2** — IBM Granite Agentic RAG. The second ship added agency. Where ship 1 retrieved and generated, ship 2 decides — when to reach for data, when to act on it, when to answer directly.
**Repo:** [a-mirror-of-my-becoming-rag-ship2-ibm-granite-agentic](https://github.com/qaevelyn/a-mirror-of-my-becoming-rag-ship2-ibm-granite-agentic)

**Ship 3** — IBM Granite RAG (standard, cross-platform). Proved the pattern could cross platforms. If the architecture only worked on one vendor's model, it was not sovereign. Same RAG pattern, different vendor, same local-first philosophy.
**Repo:** [a-mirror-of-my-becoming-rag-ship3-ibm-granite](https://github.com/qaevelyn/a-mirror-of-my-becoming-rag-ship3-ibm-granite)

**Ship 4** — IBM Granite Agentic RAG (cross-platform). Combined agency with cross-platform. Does the pattern hold when both variables change at once? IBM Granite plus agentic reasoning. The answer was yes.
**Repo:** [a-mirror-of-my-becoming-rag-ship4-ibm-granite-agentic](https://github.com/qaevelyn/a-mirror-of-my-becoming-rag-ship4-ibm-granite-agentic)

**Ship 5** — IBM Granite Agentic RAG + EvidenceFlow. The fifth ship can prove its answers. Every claim is traceable to an evidence ID. Every answer is checked against its sources. If the evidence is missing, the pipeline abstains.
**Repo:** [a-mirror-of-my-becoming-rag-ship5-ibm-granite-agentic-evidenceflow](https://github.com/qaevelyn/a-mirror-of-my-becoming-rag-ship5-ibm-granite-agentic-evidenceflow)

**Ship 6** Battle-tested, not beta-tested.  A three-component ingest pipeline for building a personal RAG vector store from exported conversation data — designed to survive the failures that kill normal pipelines: crashes, kills, wedges, and silent stalls.
**Repo** [Ship 6 — Suite: Ingestion Tools](https://github.com/qaevelyn/a-mirror-of-my-becoming-suite-ingestion-tools)** — the suite that feeds the fleet.
  
**Ship 7** of A Mirror of My Becoming™. Built October 2026 on an 8 GB Intel MacBook Air. Reads msgvault.db (SQLite mail archive), normalizes RFC822 message-ids, preserves full metadata, and feeds the canonical Chroma store with nomic-embed-text vectors — the fleet's model. The embed_gen watermark is built into msgvault's own schema: progress lives in the data itself. Crash, restart, curfew, resume — never re-ingest, never duplicate. 
**[Ship 7 — msgvault adapter](https://github.com/qaevelyn/a-mirror-of-my-becoming-suite-msgvault-adapter)** — the mail bridge.

---

## How the fleet fits together

**A Mirror of My Becoming™** is a sovereign AI practice. The RAG pipelines are one part of it. The tooling that feeds the pipelines is another. The papers are another.

- **[A Mirror of My Becoming™](https://github.com/qaevelyn/a-mirror-of-my-becoming)** — the parent index. Everything in the fleet is linked from there.
- **[Suite: Ingestion Tools](https://github.com/qaevelyn/a-mirror-of-my-becoming-suite-ingestion-tools)** — the tooling that gets documents into the vector store the pipelines read from.
- **[The Cache Is Not the Corpus](https://qaevelyn.github.io/white-papers/the-cache-is-not-the-corpus/)** — the paper on the ingestion tools' design.
- **[EvidenceFlow Verification: How Ship 5 Proves Its Answers](https://qaevelyn.github.io/case-studies/evidenceflow-verification-ship5/)** — the paper on Ship 5.
- **[Case Study: DeepSeek — The Benchmark](https://qaevelyn.github.io/white-papers/deepseek-case-study/)** — the paper that covers Ships 1–4 and the platform.
- **[The portfolio](https://qaevelyn.github.io)** — the live lookbook.

---

## Reading order

To run a pipeline:

1. Read [SETUP.md](SETUP.md) — how to point any ship at your corpus.
2. Pick a ship from the table above.
3. Read that ship's README — it names its own environment.
4. Install exactly what the ship names.
5. Run it.

To read about the fleet:

- **The ingestion tools** — [The Cache Is Not the Corpus](https://qaevelyn.github.io/white-papers/the-cache-is-not-the-corpus/).
- **Ships 1–4 and the DeepSeek platform** — [Case Study: DeepSeek — The Benchmark](https://qaevelyn.github.io/white-papers/deepseek-case-study/).
- **Ship 5 specifically** — [EvidenceFlow Verification: How Ship 5 Proves Its Answers](https://qaevelyn.github.io/case-studies/evidenceflow-verification-ship5/).
- **[Ship 6 — Suite: Ingestion Tools](https://github.com/qaevelyn/a-mirror-of-my-becoming-suite-ingestion-tools)** — the suite that feeds the fleet
- **[Ship 7 — msgvault adapter](https://github.com/qaevelyn/a-mirror-of-my-becoming-suite-msgvault-adapter)** — the mail bridge
Dedicated papers for Ships 1 through 4 individually are in the pipeline.

---

## Licensing

Every ship in the fleet is dual-licensed:

- **AGPL-3.0** — free to use, modify, and redistribute under the terms of the license.
- **Commercial license** — available for organizations that need to use the code without the AGPL-3.0 obligations. Contact the author for pricing.

Free does not mean free to exploit. If you build a product on this work, the author expects to be paid.

---

## Author

**Evelyn Caro** — Sovereign AI Builder.

**[qaevelyn.github.io](https://qaevelyn.github.io)** · Commercial licensing: **evelyn.caro.cloud@gmail.com**

---

© 2026 Evelyn Caro. All rights reserved.
