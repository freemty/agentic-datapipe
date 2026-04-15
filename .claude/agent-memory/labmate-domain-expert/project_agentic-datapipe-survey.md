---
name: Agentic Data Pipeline Survey (2026-04-15)
description: Comprehensive survey of agentic/autonomous data pipeline systems for AI training as of April 2026, covering 25+ papers and 6 open-source tools across 7 focus areas.
type: project
---

Completed a comprehensive literature survey on agentic data pipeline systems (2026-04-15).

**Why:** This is the foundational research context for the agentic-datapipe project, which aims to build an agentic orchestration layer for AI training data pipelines.

**How to apply:** Use this as the baseline for all future paper discussions, experiment design, and architecture decisions in this project.

## Key Findings

1. **The field is stratified into three layers:** orchestration (Airflow/Dagster), processing (DataTrove/NeMo Curator/Dolma), and generation (distilabel/Bespoke Curator). The missing layer is an agentic orchestrator.

2. **FT-Dojo (2026) and ALAS (2025) are the closest prior work** to a truly agentic data pipeline. FT-Dojo handles end-to-end fine-tuning autonomously; ALAS does continuous knowledge updates. Neither handles pretraining data curation.

3. **LLM-as-judge filtering is now standard practice** (FineWeb-Edu, DCLM, propella-1). The pipeline is: frontier LLM annotates quality -> small classifier distilled -> applied at scale.

4. **Self-improving loops have evolved rapidly:** Self-Instruct (2022) -> Constitutional AI (2022) -> SPIN (2024) -> DeepSeek-R1 pure RL (2025). Each step reduces human involvement.

5. **Key gap for our project:** No system exists that autonomously crawls/filters/annotates data, trains quality classifiers, evaluates downstream impact, and iterates. This is our target.

## Survey Artifacts
- Full survey: `docs/papers/agentic-datapipe-survey.md`
- Landscape table: `docs/papers/landscape.md`
