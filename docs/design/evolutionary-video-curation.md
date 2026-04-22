# Design: Evolutionary Video Data Curation for Controllable Generation

> Applying DataEvolve-style autonomous strategy evolution to video data pipelines for controllable world models (LTX 2.3, LingBot-World class).

**Date:** 2026-04-22
**Status:** Draft / Pre-experiment

---

## Motivation

DataEvolve (arXiv:2603.14420) demonstrated that autonomous evolutionary strategy design can discover category-specific data curation strategies that outperform hand-designed pipelines for LLM pretraining. The core loop — observe → design strategy → execute → evaluate → refine — is domain-agnostic.

Controllable video generation models (LingBot-World, Matrix-Game, Yume, HY-GameCraft-2) face an acute data bottleneck: high-quality action-conditioned video is scarce, and existing pipelines are hand-designed. This design explores extending evolutionary curation to this domain.

## Key Differences: Text → Video

| Dimension | DataEvolve (Text) | Video Setting |
|-----------|-------------------|---------------|
| Data unit | Document (text) | Video clip (frames + audio + caption + control signals) |
| Category | Discipline x quality (8 categories) | Content type x motion mode x control type (combinatorial) |
| Fitness validation | Train 3B LM on 500B tokens | Train video DiT — 10-100x more expensive |
| Quality dimensions | Single (text quality 1-10) | Multi: visual quality + temporal consistency + caption alignment + **control signal quality** |

The biggest bottleneck is **fitness approximation** — video model training is far too expensive for per-iteration validation.

---

## Design Space (4 Axes)

### Axis 1: Video Category Definition

How to partition video data into categories that need different curation strategies.

| Dimension | Granularity | Relevance to Controllable Generation |
|-----------|-------------|--------------------------------------|
| Content type | Nature / urban / human action / animation | Different motion patterns and noise types |
| Motion mode | Static / pan / zoom / tracking / handheld | Directly determines camera control training signal quality |
| Source | YouTube UGC / film / stock / game recording | Quality distribution varies drastically |
| Control signal type | Camera trajectory / human pose / depth / segmentation | Core differentiator for controllable gen |

**Recommended starting point:** Motion mode x control signal type (e.g., 4 motion x 2 control = 8 categories, matching DataEvolve's scale).

### Axis 2: Strategy Space

What constitutes a "curation strategy" for video data.

| Strategy Type | Operations | Examples |
|---------------|-----------|----------|
| Temporal segmentation | How to cut clips | Scene cut threshold, fixed vs adaptive length |
| Quality filtering | Keep/discard decisions | Resolution, motion score, aesthetic score thresholds |
| Caption strategy | How to describe content | Frame sampling strategy, VLM choice, camera motion description inclusion |
| Control signal extraction | What to extract, how | DUSt3R vs COLMAP, skeleton detector choice, confidence threshold |
| Control signal filtering | Quality gates on control signals | Pose estimation confidence, camera trajectory smoothness |
| Multi-dim scoring | Dimension weights | Quality vs diversity vs controllability tradeoff |

**Key reference from LingBot-World:** Their 3-layer hierarchical captioning (narrative + scene-static + dense temporal) can serve as candidate operators in the strategy space. Different categories may need different captioning combinations.

**Key reference from HY-GameCraft-2:** Dual captioning (standard + interaction-diff) captures causal state transitions — a novel operator for interactive data.

### Axis 3: Fitness Approximation (Critical Design Choice)

| Proxy | GPU Cost | Signal Reliability | Applicability |
|-------|----------|-------------------|---------------|
| VLM-as-judge (VLM scores data quality) | ~0 GPU (API) | Low — VLM doesn't know what helps generative models | Initial screening, inner evolution loop |
| CLIP/ViCLIP score | Very low | Medium — text-video alignment OK, but not controllability | Fast filtering |
| Control accuracy metric (extract control signal, check consistency) | Low | Medium — directly measures control signal quality | **Unique to controllable gen** |
| Small model probe (train small video DiT, measure FVD/FID) | 4-8 GPU x days | High — most direct but most expensive | Final validation, every N iterations |
| **Hybrid: VLM + control metric for evolution, small probe for validation** | Mixed | Best overall | **Recommended** |

**Key gap identified:** LingBot-World uses VBench (passive video quality) but has zero quantitative action faithfulness evaluation. This is a contribution opportunity.

Proposed composite fitness:
```
Fitness = w1 * VLM_quality_score
        + w2 * action_faithfulness_score   (camera trajectory consistency)
        + w3 * diversity_score             (category coverage)
        + w4 * small_model_probe_loss      (downstream proxy, periodic)
```

### Axis 4: Evolution Mechanism

| Approach | Complexity | Advantage |
|----------|-----------|-----------|
| DataEvolve original (single-parent mutation + selection) | Low | Proven, sufficient |
| Multi-objective evolution (Pareto front across quality dimensions) | Medium | Natural fit for video's multi-dimensional quality |
| Population-based (multiple strategies + crossover) | High | May discover better combinations |

---

## Feasibility Plan (16 GPU Constraint)

### Resource Allocation

```
16 GPU budget:
├── 4 GPU (continuous): control signal extraction (DUSt3R/pose estimation)
├── 4 GPU (on-demand): VLM captioning (InternVL-2 or Qwen2-VL)
└── 8 GPU (periodic):  small video DiT validation training
```

### Phase 1: Framework Validation (2-3 weeks, minimal GPU)

Run evolutionary loop via API:
- Input: Panda-70M or OpenVid-1M subset (~100K clips)
- Categories: 4-8 by motion type
- Strategy space: filtering thresholds + caption strategy
- Fitness: VLM-as-judge + CLIP score (pure API)
- Output: evolved strategy per category
- **Key question:** Does the loop converge to meaningful strategies?

### Phase 2: Control-Aware Evolution (2-3 weeks, 4-8 GPU)

Introduce controllability dimension:
- Extract camera trajectories via DUSt3R/MASt3R (4 GPU)
- Define control signal quality score (smoothness, confidence, coverage)
- Add to evolution loop as fitness dimension
- Compare: with vs without control-aware filtering

### Phase 3: Small Model Validation (3-4 weeks, 8 GPU)

- Train small video DiT (~500M-1B params, LTX-Video small variant)
- Compare evolved strategies on: FVD, CLIP-score, **camera control accuracy**
- Short training (~50K steps), test statistical significance

### Critical Ablations

| Exp | Question | Cost |
|-----|----------|------|
| A1: Cleaning vs Transformation | Does DataEvolve's core finding hold for video? | 8 GPU x 3 runs |
| A2: Control-aware filtering | How much does control signal quality filtering improve controllability? | 8 GPU x 2 runs |
| A3: VLM-judge vs actual FVD rank correlation | Can we trust cheap proxies? | 8 GPU x 5-8 short runs |
| A4: Category-specific vs universal strategy | Do different motion types really need different strategies? | 8 GPU x 2 runs |

---

## Expected Contributions

1. **Cross-modal validation of evolutionary curation** — first evidence of whether DataEvolve works for video
2. **Video fitness proxy design** — which VLM + control metric combo correlates with real FVD
3. **Control signal quality as filtering dimension** — directly actionable for LTX/LingBot-World class models
4. **Cleaning vs transformation in video** — DataEvolve found cleaning > transformation for text; video may differ (caption quality has outsized impact)

## Key References

- DataEvolve (arXiv:2603.14420) — evolutionary strategy design framework
- LingBot-World (arXiv:2601.20540) — 3-source data engine + 3-layer captioning reference
- Matrix-Game 2.0 (arXiv:2508.13009) — most precise action annotation pipeline
- HY-GameCraft-2 (arXiv:2511.23429) — most innovative captioning (dual: standard + interaction-diff)
- Yume (arXiv:2507.17744) — QCM camera quantization; fully open data/code/weights
- Cosmos WFM (arXiv:2501.03575) — largest scale pipeline (20M hrs → 100M clips)

## Trade-offs

| Choice | Pro | Con |
|--------|-----|-----|
| Start with camera control only | Tractable, verifiable with LTX 2.3 | Narrow scope |
| Multi-modal control (camera + pose + depth) | Higher impact | Engineering-heavy, hard to validate |
| Use Yume's open data as testbed | Free, reproducible | Limited to walking/drone footage |
| Build custom game data collection | Precise GT labels for validation | High setup cost, 16 GPU not enough |
