---
name: Image/Video Generation Data Pipeline Survey
description: Comprehensive survey of data pipelines for training image and video generation models (Stable Diffusion, Sora, CogVideoX, etc.) covering LAION-5B, DataComp, video captioning (ShareGPT4Video, Panda-70M, InternVid), filtering techniques, and open-source tools (img2dataset, video2dataset, Open-Sora)
type: project
---

Completed a thorough literature survey on data pipelines for image and video generation models (2026-04-15).

**Why:** The agentic-datapipe project needs to understand the full landscape of how generative AI models prepare their training data, from web-scale image-text curation (LAION-5B) to video-specific challenges (scene detection, motion scoring, temporal consistency).

**How to apply:** Use this knowledge to inform architecture decisions for the video data pipeline. Key references are Open-Sora Plan (multi-dimensional filtering), ShareGPT4Video (VLM captioning at scale), and Data Filtering Networks (learned vs heuristic filtering).

**Key findings:**
- 18+ papers and 8+ tools surveyed; written to docs/papers/data-pipelines-survey.md
- landscape.md updated with sections 7-10 covering image gen pipelines, video datasets, video gen models, and video tools
- The canonical video pipeline: scene-split -> hard-filter -> safety-filter -> motion-score -> aesthetic-score -> CLIP-align -> caption -> dedup
- Biggest gap: no unified open-source video data pipeline framework (each project rolls their own)
- VLM captioning (GPT-4V gold -> distill to lighter captioner) is the dominant 2024+ pattern
- Data Filtering Networks showed learned filtering > heuristic filtering for images; unexplored for video
