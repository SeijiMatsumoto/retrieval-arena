# Study 1: context strategies for document question answering

Status: initial design. The research scope and comparison families are agreed; choices marked
proposed or open below are not settled experiment settings. No paid runs are authorized by this file.

## 1. Problem and decision

Choose how to supply evidence from a document collection to an LLM answering questions. Find the
conditions under which long context, fixed retrieval, or iterative retrieval delivers the best
quality for an acceptable cost and latency. This is a general document-QA study, not story matching.

## 2. Hypothesis

Exploratory. A working hypothesis is that the tradeoff changes with corpus size and evidence
dispersion: full context may be sufficient for small collections, while retrieval and additional
search steps may help as irrelevant content and multi-document questions increase. This is a
hypothesis to test, not a claimed result.

## 3. Baseline and contenders

Planned: long context, basic RAG, hybrid RAG, reranked RAG, and agentic RAG. Proposed diagnostic
baselines: no-context answering and oracle evidence (where available). Begin with long context,
basic RAG, and agentic RAG; add the others after the shared evaluation path works.

Hold the answering model, question set, source collection, answer schema, and evaluator constant.
Record prompts, model versions, chunking, indexes, context limits, top-k, tool budgets, and seeds.
Agent planning/search calls are additional computation and must be included in accounting; this
is a strategy comparison, not a claim of identical compute.

## 4. Dataset and experimental unit

Open: select a public document-QA dataset with attributable reference answers and evidence
locations, compatible redistribution terms, and an auditable acquisition path. No dataset is
selected or copied yet. Include single-document, multi-document, and unanswerable cases where
credible labels exist. Record any separately constructed cases as such.

Proposed schema: corpus/document IDs and frozen text/hash; question ID, question, split, reference
answer(s), evidence document/passage IDs, answerability, and scenario tags. Reference fields must
be evaluator-only. Contenders receive only the question and permitted corpus/tool access.

Use source/corpus-grouped development and held-out splits to reduce leakage. Define corpus-size
slices and distractor sampling before testing. Keep questions and required evidence comparable
across methods within each slice; report overflow rather than silently truncating long context.

## 5. Correctness and labels

Open: answer scoring and evidence-support protocol, based on the chosen dataset. Preserve its
original label provenance; document any human or model review and disagreements. Separate answer
correctness, citation validity, semantic support, and evidence recall. Do not treat citation
location checks alone as proof that an answer is supported.

Treat errors/timeouts as failures with explicit accounting. Evaluate unanswerable cases and
false/confident answers separately. Tune prompts/evaluators only on development data.

## 6. Metrics and selection

Proposed primary outcome: supported answer correctness, with the precise scoring rule still open.
Diagnostics: answer correctness, evidence recall, citation support, abstention behavior, per-scenario
quality, and failure rate. Report fresh end-to-end p50/p95 latency, total API cost per question,
cache usage, and one-time ingestion/indexing cost separately. Unknown cost remains unknown.

Open: practical quality margin, reliability thresholds, cost and latency limits, and repeat count.
Until these are agreed, report tradeoffs rather than selecting a winner. Once frozen, select
eligible configurations with a deterministic rule; allow no eligible method and inconclusive
results. Use uncertainty analysis paired on the same questions and grouped at the independent
source/corpus unit as appropriate. Non-significance does not establish equivalence.

## 7. Scope, budget, and deliverables

Current scope: clean repository foundation and study design. Next: select data and evaluation
protocol, build an offline fixture and shared runner, implement the first three approaches,
validate scoring and budget accounting, then estimate and authorize a small live pilot.

Open: exact models, API prices, sample size, labeling/judging costs, and authorized spending cap.
Do not carry forward the former dedup study's dollar estimate. No paid calls, data exports,
production changes, or benchmark claims are part of this repository setup.

After real evaluation: dated reports, reproducible config, label provenance, limitations, and
arena-summary/1 output for the Arenas hub. No placeholder/mock result should appear as a finding.
