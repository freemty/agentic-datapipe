---
name: Embodied AI Data Pipeline Survey (April 2026)
description: Comprehensive survey of data pipelines for robotics foundation models -- VLA models, cross-embodiment data standards, video-to-action methods, collection hardware, VLM annotation, simulation generation
type: project
---

Completed a full literature survey on data pipelines for embodied AI / robotics foundation models, covering 22+ papers (2022-2026).

**Why:** User is researching the connection between video understanding and action prediction for robotics, with focus on how data is collected, standardized, augmented, and used to train robot foundation models.

**How to apply:** This survey covers 7 sub-topics: (1) Robot foundation model data (RT-X, Octo, OpenVLA, pi0, GR00T N1, RDT-1B, ABot-M0), (2) Open X-Embodiment cross-embodiment standard, (3) Internet video for robot learning (R3M, VIP, UniPi, GR-1, VidBot, Magma), (4) Collection hardware (ALOHA, UMI, DROID), (5) VLM/LLM annotation (ROSIE, Interleave-VLA), (6) Simulation (RoboCasa, ManiSkill), (7) Video-to-action gap analysis.

Key files:
- Full survey: docs/papers/embodied-ai-data-pipelines-survey.md
- Landscape updated: docs/papers/landscape.md (Section 6)

Key insights:
- RLDS/Open X-Embodiment is the de facto data standard but action space unification remains unsolved
- Three macro-trends: dataset unification, VLA models inheriting VLM knowledge, scalable data flywheels
- The video-to-action gap has 5 main solution approaches: visual pre-training, world models, subgoal generation, 3D affordance extraction, VLM semantic bridge
- UMI ($200 handheld device) is most scalable collection method; DROID is most diverse (564 scenes)
- ABot-M0 (2026) represents state-of-the-art with full systematic curation pipeline + Action Manifold Learning
