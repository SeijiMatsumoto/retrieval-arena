# Retrieval Arena

This is a new general document-QA experiment, separate from `../dedup-arena`.
Read README.md and EXPERIMENT.md before implementation. The current repository is a study design,
not a working pipeline. Do not invent measured results or copy dedup-specific schemas/scoring.

Use appropriate arena-kit components. The default classification scaffold is not a QA evaluator.
Freeze dataset provenance, held-out splits, scoring and decision rules before real evaluation.
Keep evaluator-only answers/evidence out of contender inputs. Count iterative search calls in
cost/latency. Run offline checks first; paid calls require an explicit budget authorization.
Publish a hub summary only when a real, attributable snapshot exists.
