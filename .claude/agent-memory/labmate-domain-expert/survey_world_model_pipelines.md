---
name: World Model Data Pipeline Survey
description: Comprehensive survey of 39 papers on world models, world action models, latent action models, and their training data pipelines as of April 2026. Covers game WMs (GameNGen, DIAMOND, Solaris, COMBAT, Matrix-Game 3.0), robot WMs (DreamDojo, PlayWorld, Cosmos Policy), WAMs (VAG, DiT4DiT, Veo-Act, VLAW), latent action models (Garrido/Meta finding VQ fails on diverse video, AC-LAM, HiLAM, FLAM, Olaf-World), synthetic data pipelines (ComSim, SIM1, RoboCurate), agentic data collection (PlayWorld self-play, Action100M automated annotation), and action tokenization debate (continuous > discrete).
type: project
---

## Key Findings (April 2026)

**Three macro-trends:**
1. Data pipeline is the product -- papers increasingly describe data engines, not just models
2. Latent actions as universal interface -- learning action spaces from unlabeled video (8+ competing approaches)
3. Closed-loop data flywheels -- WM generates data -> trains policy -> rollouts improve WM (VLAW pattern)

**Why:** The central bottleneck in world models shifted from architecture to data quality/diversity/action-conditioning.

**How to apply:** When discussing world model data pipelines, reference these three trends. The VLAW flywheel pattern is the most complete agentic data pipeline for world models.

## Critical Technical Findings
- VQ action tokenization (Genie-style) **fails on diverse in-the-wild video** (Garrido et al., Meta, 2026) -- continuous constrained latent actions are better
- Co-training study (Lin et al., 2026): discrete action token variants yield **no significant benefit** in VLA training
- DreamDojo: largest WM pretraining dataset is 44k hours egocentric human video
- PlayWorld: first fully autonomous robot self-play WM (no demos needed)
- Veo-Act: commercial video model (Veo-3) as zero-shot robot planner + lightweight IDM from random-play data only
- Action100M: fully automated annotation of 100M+ video segments (V-JEPA 2 + GPT-class reasoning)
- SIM1: physics-aligned sim achieves 90% zero-shot, 1:15 real-synthetic equivalence ratio

## Files
- Full survey: `docs/papers/world-model-data-pipeline-survey.md`
- Landscape tables: `docs/papers/landscape.md` (sections 6-WM through 6-DS)
