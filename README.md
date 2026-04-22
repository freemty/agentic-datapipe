# agentic-datapipe

Agentic data pipeline for video/world model training data — applying autonomous, evolutionary curation strategies to build high-quality datasets for controllable video generation.

## Problem

Training controllable video generation models (LTX, LingBot-World, Matrix-Game class) requires action-conditioned video data that is:
- Precisely annotated with camera trajectories and control signals
- Filtered for visual quality, temporal consistency, and control signal clarity
- Categorized by content type, motion mode, and control type

Current data pipelines are hand-designed, one-shot processes. No existing tool combines large-scale internet video with precise action annotation, general-domain coverage, and iterative quality refinement.

## Approach

Extend [DataEvolve](https://arxiv.org/abs/2603.14420)-style evolutionary strategy design to video data curation:

```
Observe data → Design strategy → Execute curation → Evaluate fitness → Refine
     ↑                                                                    |
     └────────────────────────────────────────────────────────────────────┘
```

Key design axes:
1. **Category definition** — partition video by motion mode x control signal type
2. **Strategy space** — temporal segmentation, quality filtering, captioning strategy, control signal extraction/filtering
3. **Fitness approximation** — hybrid VLM-as-judge + control accuracy metric + periodic small model probe
4. **Evolution mechanism** — iterative refinement with cross-generation knowledge transfer

## Project Structure

```
docs/
  papers/          # Literature surveys and landscape map
    landscape.md   # Master literature map (7 sections, 100+ papers)
  design/          # Design documents
exp/               # Experiment tracking
scripts/           # Experiment orchestration
viewer/            # Results viewer
```

## Documentation

| Document | Description |
|----------|-------------|
| [Literature Landscape](docs/papers/landscape.md) | Domain literature map covering data curation, world models, video generation pipelines |
| [Evolutionary Video Curation Design](docs/design/evolutionary-video-curation.md) | Design space: 4 axes, 16 GPU feasibility plan, critical ablations |
| [Video Pipeline Tools Survey](docs/design/video-pipeline-tools.md) | Survey of 11 open-source tools (Cosmos-Curate, video2dataset, etc.) |
| [CHANGELOG](CHANGELOG.md) | Version history |

## Key References

- [DataEvolve](https://arxiv.org/abs/2603.14420) — Autonomous evolutionary strategy design for data curation
- [LingBot-World](https://arxiv.org/abs/2601.20540) — 3-source data engine + 3-layer hierarchical captioning
- [Matrix-Game 2.0](https://arxiv.org/abs/2508.13009) — Most precise action annotation pipeline (ms-level sync)
- [HY-GameCraft-2](https://arxiv.org/abs/2511.23429) — Dual captioning (standard + interaction-diff)
- [Yume](https://arxiv.org/abs/2507.17744) — QCM camera quantization; fully open data/code/weights
- [Cosmos WFM](https://arxiv.org/abs/2501.03575) — Largest scale pipeline (20M hrs raw video)

## Status

Early research phase. Literature survey and design space exploration complete. No experiments yet.

## License

TBD
