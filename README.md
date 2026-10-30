# Retrieval Arena

**Long context, RAG, and agentic RAG compared on the same document questions: answer quality, evidence support, latency, and cost.**

Which approach gives an LLM the context it needs to answer accurately? This project will measure
where each approach earns its overhead, across question types and corpus sizes. The goal is
workload-specific guidance, not a universal winner.

**Status: study design. No comparison pipeline, selected benchmark, or measured results yet.**
See [EXPERIMENT.md](EXPERIMENT.md) for the initial study and open decisions.

## Planned comparison

| Approach | How it obtains context |
|---|---|
| Long context | All documents in a shared corpus slice, within the model's context limit |
| Basic RAG | One search retrieves a fixed set of chunks |
| Hybrid RAG | Keyword and embedding retrieval combined |
| Reranked RAG | A larger retrieved pool is reranked before answering |
| Agentic RAG | The model searches iteratively within an explicit tool and token budget |

The initial comparison will hold the answering model, document collection, questions, answer
format, and evaluation protocol constant. Retrieval and agent calls count toward total cost and
latency. Evidence retrieval and final answer quality will be measured separately.

## What happened to the previous project?

The former `retrieval-arena` measured **news story deduplication**. It moved, with its history,
dataset, and results, to **[Dedup Arena](https://github.com/SeijiMatsumoto/dedup-arena)**.

- [Existing measured results](https://github.com/SeijiMatsumoto/dedup-arena/tree/main/snapshots/2026-10-27_2053)
- [Dedup source and reproduction commands](https://github.com/SeijiMatsumoto/dedup-arena)

Because this repository reuses the old name, old deep links do not automatically redirect.
Replace `SeijiMatsumoto/retrieval-arena` with `SeijiMatsumoto/dedup-arena` in links to the old study.

## Shared infrastructure

The implementation will reuse appropriate parts of [arena-kit](https://github.com/SeijiMatsumoto/arenas/tree/main/kit)
for cached provider calls, statistics, and the hub summary contract. Answer evaluation will need
study-specific scoring rather than the kit's default classification scaffold.

## Caveats

- Planned approaches are not implemented or benchmark findings.
- Dataset selection, label provenance, evaluation thresholds, model configuration, and paid-run
  budget remain open. They must be recorded before a real evaluation.
- A correct answer without supporting evidence is different from a supported correct answer.
- Long-context overflow must be reported explicitly; silently truncating the corpus would change
  the comparison.
