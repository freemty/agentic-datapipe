---
name: LLM Data Pipeline Survey Findings
description: Key findings from April 2026 survey of automated data pipelines for LLM/VLM training -- model-based filtering, DoReMi mixing, synthetic data scaling
type: project
---

Completed comprehensive survey of automated data pipelines for LLM/VLM training (April 2026).

**Why:** Establishing foundation knowledge for the agentic-datapipe project. This survey covers 33+ papers across 5 research axes.

**How to apply:** Use these findings to guide pipeline design decisions. Key architectural choices should reference this survey.

Key findings:
1. Model-based filtering (DCLM 2024) is now the established SOTA -- fastText quality classifiers trained on high-quality refs outperform all heuristic methods
2. DoReMi (proxy model DRO) is the go-to for automated data mixing -- 280M proxy decides for 8B model, 2.6x speedup
3. Synthetic pretraining data has reached trillion-token scale -- BeyondWeb (2025) outperforms Cosmopedia/Nemotron-Synth by 2-5pp
4. Token-level filtering (OpenAI, 2026) is the emerging frontier -- finer granularity than document-level
5. Data-Quality Illusion paper (2025) warns that classifiers may capture topic distribution rather than actual quality
6. FineWeb2 (2025) is the first auto-adapted multilingual pipeline for 1000+ languages
7. No fully end-to-end automated pipeline exists yet -- each stage has good solutions but integration is an open problem

Survey files:
- Full survey: docs/papers/automated-data-pipelines-survey.md
- Landscape updated: docs/papers/landscape.md (sections 1, 1b, 2)
