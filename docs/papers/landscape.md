# Literature Landscape: Agentic Data Pipelines for AI Training

**Last updated:** 2026-04-15

---

## 1. Large-Scale Pretraining Data Curation

| Paper | Year | Type | Key Method | Our Relevance |
|-------|------|------|------------|---------------|
| [DCLM](https://arxiv.org/abs/2406.11794) | 2024 | Preprint | Benchmark for data curation; 240T pool; model-based filtering key | **Core reference** -- eval framework |
| [FineWeb / FineWeb-Edu](https://arxiv.org/abs/2406.17557) | 2024 | Preprint | 15T English tokens; LLM-annotated quality classifier | Baseline quality filtering |
| [FineWeb2](https://arxiv.org/abs/2506.20920) | 2025 | Preprint | Auto-adapted multilingual; 1000+ langs; 20TB | Key multilingual automation ref |
| [RefinedWeb](https://arxiv.org/abs/2306.01116) | 2023 | Preprint | Web-only matches curated corpora; 5T tokens from CC | Proved web-only viable |
| RedPajama v1/v2 | 2023 | Open-source | Open LLaMA recipe; v2: 30T+ with quality signals | Quality signal design ref |
| [propella-1](https://arxiv.org/abs/2602.12414) | 2026 | Preprint | Multi-property document annotation at scale | Multi-axis quality |
| [Dolma](https://github.com/allenai/dolma) | 2024 | Open-source | Rust+Python curation toolkit, 3T tokens | Processing backend |
| [GPT-4o Quality Filter](https://arxiv.org/abs/2410.02755) | 2024 | Preprint | Frontier LLM annotates, small model distills | Quality classifier technique |
| [Pretrainer's Guide](https://arxiv.org/abs/2305.13169) | 2023 | Preprint | Study of data age/quality/toxicity/domain | Experimental design ref |
| [Ultra-FineWeb](https://arxiv.org/abs/2505.05427) | 2025 | Preprint | Verification layers on FineWeb pipeline | Improved filtering |
| [AICC](https://arxiv.org/abs/2511.16397) | 2025 | Preprint | Model-based HTML parsing; 7.3T corpus | Extraction quality matters |
| [Token-Level Filtering](https://arxiv.org/abs/2601.21571) | 2026 | Preprint (OpenAI) | Per-token capability shaping | Frontier granularity |
| [Data-Quality Illusion](https://arxiv.org/abs/2510.00866) | 2025 | Preprint | Classifiers capture topic not quality; over-filtering risk | Filter design warning |
| [Data Quality Scaling Laws](https://arxiv.org/abs/2510.03313) | 2025 | Preprint | Quality-adjusted Chinchilla scaling laws | Value estimation |
| [Safety Filtering](https://arxiv.org/abs/2505.02009) | 2025 | Preprint | Harmful content filtering at pretraining level | Safety component |
| [Dataset Fingerprints](https://arxiv.org/abs/2412.02857) | 2024 | NeurIPS 2025 | Filtering leaves fingerprints in models | Pipeline effect analysis |
| [Mix, MinHash, Match](https://arxiv.org/abs/2512.18834) | 2025 | Preprint | Cross-source agreement as quality signal | Novel quality signal |
| [Multilingual Quality](https://arxiv.org/abs/2505.22232) | 2025 | Preprint | Cross-lingual quality judges | Multilingual pipeline ref |
| [DataEvolve](https://arxiv.org/abs/2603.14420) | 2026 | Preprint | Autonomous evolutionary strategy design; beats DCLM/FineWeb-Edu on 18 benchmarks; cleaning > transformation | **Core reference** -- automated strategy discovery (see also §3) |

## 1b. Data Mixing & Selection

| Paper | Year | Type | Key Method | Our Relevance |
|-------|------|------|------------|---------------|
| [DoReMi](https://arxiv.org/abs/2305.10429) | 2023 | NeurIPS 2023 | Proxy model DRO for domain reweighting; 2.6x speedup | **Core mixing method** |
| [DSIR](https://arxiv.org/abs/2302.03169) | 2023 | NeurIPS 2023 | Importance resampling with hashed n-grams | Selection method reference |
| [Topic Over Source](https://arxiv.org/abs/2502.16802) | 2025 | Preprint | Topic-based mixing outperforms source-based | Challenges standard mixing assumption |
| [Scaling Laws for Data Mixtures](https://arxiv.org/abs/2507.09404) | 2025 | Preprint | Predicts optimal mix from compute budget | Principled mix decisions |
| [QuaDMix](https://arxiv.org/abs/2504.16511) | 2025 | Preprint | Quality-diversity balance in selection | Addresses diversity collapse |
| [MuRating](https://arxiv.org/abs/2507.01785) | 2025 | NeurIPS 2025 | Cross-lingual quality transfer for 17 languages | Multilingual selection |

## 2. Synthetic Data Generation & Self-Improving Loops

| Paper | Year | Type | Key Method | Our Relevance |
|-------|------|------|------------|---------------|
| [Self-Instruct](https://arxiv.org/abs/2212.10560) | 2022 | ACL 2023 | Bootstrap instruction data from seed tasks | Foundation for synthetic generation |
| [Evol-Instruct / WizardLM](https://arxiv.org/abs/2304.12244) | 2023 | Preprint | Evolutionary instruction complexity scaling | Instruction evolution paradigm |
| [Constitutional AI](https://arxiv.org/abs/2212.08073) | 2022 | Preprint | Self-critique/revision loop; RLAIF from principles | Autonomous safety data curation |
| [phi-1 (Textbooks)](https://arxiv.org/abs/2306.11644) | 2023 | Preprint | Synthetic textbook data; quality >> quantity | Validates synthetic data approach |
| [Phi-3](https://arxiv.org/abs/2404.14219) | 2024 | Preprint | 3.8B on 3.3T tokens; heavily filtered + synthetic | Scaled synthetic pretraining |
| [Nemotron-4 340B](https://arxiv.org/abs/2406.11704) | 2024 | Preprint | 98% synthetic alignment; self-gen pipeline | Industrial synthetic pipeline |
| [Cosmopedia](https://huggingface.co/datasets/HuggingFaceTB/cosmopedia) | 2024 | Dataset | Mixtral-generated textbooks for pretraining | Open synthetic data reference |
| [BeyondWeb](https://arxiv.org/abs/2508.10975) | 2025 | Preprint | Outperforms Cosmopedia/Nemotron; 7.7x faster than web | **SOTA synthetic pretraining** |
| [BhashaKritika](https://arxiv.org/abs/2511.10338) | 2025 | Preprint | Synthetic pretraining for low-resource Indic languages | Multilingual synthetic ref |
| [FineInstructions](https://arxiv.org/abs/2601.22146) | 2026 | Preprint | Synthetic instructions at pretraining scale | Bridges instruct-tuning and pretraining |
| [DS2-Instruct](https://arxiv.org/abs/2603.12932) | 2026 | Preprint | Domain-specific synthetic data synthesis | Domain adaptation |
| [Seed-Coder](https://arxiv.org/abs/2506.03524) | 2025 | Preprint | Code model curates its own pretraining data | Self-curating paradigm |
| [SPIN](https://arxiv.org/abs/2401.01335) | 2024 | ICML 2024 | Self-play generates preference data iteratively | Self-improving loop |
| [DeepSeek-R1](https://arxiv.org/abs/2501.12948) | 2025 | Nature | Pure RL for reasoning; emergent patterns distilled | No labeled data needed |
| [Synthetic Data Quality Survey](https://arxiv.org/abs/2412.02580) | 2024 | Preprint | Quality/diversity/complexity as independent axes | Evaluation framework |
| [RLSF](https://arxiv.org/abs/2507.17284) | 2025 | Preprint | Self-feedback for calibration | Self-evaluation technique |

## 3. Agentic Data Pipeline Systems

| Paper | Year | Type | Key Method | Our Relevance |
|-------|------|------|------------|---------------|
| [FT-Dojo / FT-Agent](https://arxiv.org/abs/2603.01712) | 2026 | Preprint | End-to-end autonomous fine-tuning agent | **Closest prior work** -- extend to pretraining |
| [ALAS](https://arxiv.org/abs/2508.15805) | 2025 | Preprint | Continuous knowledge update agent; curriculum + retrieval + distillation + fine-tune | Continuous learning architecture reference |
| [ADMA Copilot](https://arxiv.org/abs/2411.00188) | 2024 | Preprint | Multi-agent data management; meta-program graph | Agent orchestration pattern |
| [Materials DB Agents](https://arxiv.org/abs/2602.03069) | 2026 | Preprint | Skill-based agent for PDF extraction; cross-modal verification | Domain-specific extraction at scale |
| [Material Property Extraction](https://arxiv.org/abs/2510.01235) | 2025 | Published | Multi-agent extraction from 10K papers | Multi-agent extraction architecture |
| [DataEvolve / Data Darwinism II](https://arxiv.org/abs/2603.14420) | 2026 | Preprint | Evolutionary loop for autonomous data curation strategy discovery; 4-agent system (observer→designer→cleaner→judge) with experience pool + strategy pool; 30 generations per category on 672B tokens → Darwin-CC 504B tokens; 3B model beats DCLM/FineWeb-Edu/Ultra-FineWeb; discovers cleaning > transformation | **Key reference** -- evolutionary strategy optimization for data pipeline; extend to video/multi-modal |

## 4. Open-Source Tools

| Tool | Stars | Maintainer | Layer | Key Capability |
|------|-------|-----------|-------|---------------|
| [DataTrove](https://github.com/huggingface/datatrove) | 3.0k | HuggingFace | Processing | Platform-agnostic pipeline blocks; dedup; LLM-integrated |
| [NeMo Curator](https://github.com/NVIDIA/NeMo-Curator) | 1.5k | NVIDIA | Processing | GPU-accelerated multi-modal; 16x faster dedup |
| [distilabel](https://github.com/argilla-io/distilabel) | 3.2k | Argilla | Generation | Synthetic data + AI feedback; research paper implementations |
| [Bespoke Curator](https://github.com/bespokelabsai/curator) | 1.7k | Bespoke Labs | Generation | Bulk LLM inference; structured output; cost-optimized |
| [Dolma](https://github.com/allenai/dolma) | 1.5k | AI2 | Processing | Rust-based; reproducible curation toolkit |
| [DCLM](https://github.com/mlfoundations/dclm) | 1.4k | ML Foundations | Benchmark | Standardized evaluation for data curation strategies |

## 5. Preference Learning & Reward Data

| Paper | Year | Type | Key Method | Our Relevance |
|-------|------|------|------------|---------------|
| [Constitutional AI (RLAIF)](https://arxiv.org/abs/2212.08073) | 2022 | Preprint | AI preference labels from principles | Autonomous preference data generation |
| [DPO](https://arxiv.org/abs/2305.18290) | 2023 | NeurIPS | Direct optimization from preferences | Simplified preference training pipeline |
| [IPO / Psi-PO](https://arxiv.org/abs/2310.12036) | 2023 | Preprint | General preference optimization framework | Theoretical foundation |
| [SPIN](https://arxiv.org/abs/2401.01335) | 2024 | ICML | Self-play preference generation | Self-improving preference data |

---

## 6. World Models, World Action Models, and Action-Conditioned Data Pipelines

*Full survey: [world-model-data-pipeline-survey.md](./world-model-data-pipeline-survey.md)* | *Interactive world model reports: [interactive-world-models-survey.md](./interactive-world-models-survey.md)*

### 6-WM. World Models (Game Domain)

| Paper | Year | Venue | Data Pipeline | Action Repr. | Key Numbers |
|-------|------|-------|---------------|-------------|-------------|
| [GameNGen](https://arxiv.org/abs/2408.14837) | 2024 | Preprint | RL agent auto-play (900M frames) | Game controls | Real-time DOOM |
| [DIAMOND](https://arxiv.org/abs/2405.12399) | 2024 | NeurIPS Spotlight | Atari replay buffers | Discrete game actions | SOTA Atari WM |
| [GameGen-X](https://arxiv.org/abs/2411.00769) | 2024 | Preprint | 150+ game recordings (1M+ clips); GPT-4o captioning; InstructNet for multi-modal control | Keyboard + mouse + semantic instruction | First open-world game video gen |
| [Cosmos WFM](https://arxiv.org/abs/2501.03575) | 2025 | Preprint (NVIDIA) | 20M hrs raw video → 5-stage pipeline (TransNetV2 split → multi-stage filter → VLM caption → semantic dedup → sharding) → 100M clips | Camera pose (post-train); robot actions | Foundation WM platform; up to 4K |
| [Matrix-Game v1](https://arxiv.org/abs/2506.18701) | 2025 | Preprint | Minecraft 3700hrs (2700 unlabeled + 1000 labeled); frame-level keyboard+mouse | Frame-level keyboard + mouse | 17B params; GameWorld Score benchmark |
| [Matrix-Game 2.0](https://arxiv.org/abs/2508.13009) | 2025 | Preprint | UE NavMesh + GTA5 ScriptHook + PPO agents; ~1200hrs produced; ms-precision action sync; >99% accuracy | Frame-level keyboard + mouse (ms) | 25FPS real-time; open weights+code |
| [Yume](https://arxiv.org/abs/2507.17744) | 2025 | Preprint | Sekai dataset: 11K hrs YouTube → 400hrs HQ; MegaSAM camera; QCM quantization → discrete keyboard actions | Quantized camera motion as text | 1080p; fully open (data+code+weights) |
| [HY-GameCraft-2](https://arxiv.org/abs/2511.23429) | 2025 | Preprint (Tencent) | 150+ AAA games; dual captioning (standard + interaction-diff); 150K synthetic via VLM+image-edit; VIPE 6DoF camera | Text instruction + keyboard + mouse | 14B MoE; 16FPS; most innovative caption |
| [Solaris](https://arxiv.org/abs/2602.22208) | 2026 | Preprint | Automated multi-agent collection (12.64M frames) | Minecraft controls | First multiplayer WM |
| [LingBot-World](https://arxiv.org/abs/2601.20540) | 2026 | Preprint | 3-source (internet video + game platform + UE synthetic); 3-level profiling; 3-layer hierarchical captioning (narrative + scene-static + dense temporal JSON) | Plücker 6DoF + WASD multi-hot | 28B MoE; 16FPS; emergent memory 60s+ |
| [COMBAT](https://arxiv.org/abs/2603.00825) | 2026 | Preprint | Single-player inputs only | Partial action labels | Emergent opponent behavior |
| [Infinite-World](https://arxiv.org/abs/2602.02393) | 2026 | Preprint | Uncertainty-aware action labeling | Tri-state discrete | 1000+ frame consistency |
| [Matrix-Game 3.0](https://arxiv.org/abs/2604.08995) | 2026 | Preprint | Industrial data engine (UE5 + AAA + real) | Pose-Action-Prompt quad | 720p@40FPS real-time |

### 6-WM-R. World Models (Robotics)

| Paper | Year | Venue | Data Pipeline | Action Repr. | Key Numbers |
|-------|------|-------|---------------|-------------|-------------|
| [DreamDojo](https://arxiv.org/abs/2602.06949) | 2026 | Preprint | 44k hr egocentric human video + robot fine-tune | Continuous latent | Largest WM pretraining |
| [PlayWorld](https://arxiv.org/abs/2603.09030) | 2026 | Preprint | Autonomous robot self-play (no demos) | Robot actions | 65% policy improvement |
| [Cosmos Policy](https://arxiv.org/abs/2601.16163) | 2026 | Preprint (NVIDIA) | Robot demos -> post-train video model | Actions as latent frames | 98.5% LIBERO |
| [Genie](https://arxiv.org/abs/2402.15391) | 2024 | Preprint (DeepMind) | Internet video (no action labels) | VQ discrete latent | First latent action WM |
| [ABot-PhysWorld](https://arxiv.org/abs/2603.23376) | 2026 | Preprint | Interactive robot data | Multi-modal | Foundation WM for manipulation |

### 6-WAM. World Action Models (Joint Video+Action Generation)

| Paper | Year | Venue | Data Pipeline | Architecture | Key Numbers |
|-------|------|-------|---------------|-------------|-------------|
| [VAG](https://arxiv.org/abs/2604.09330) | 2026 | Preprint | Paired (video, action) demos | Dual-stream flow-matching | Aligned video-action pairs |
| [DiT4DiT](https://arxiv.org/abs/2603.10448) | 2026 | Preprint | Robot demos | Cascaded video DiT + action DiT | 98.6% LIBERO, 10x efficiency |
| [Veo-Act](https://arxiv.org/abs/2604.04502) | 2026 | Preprint | Zero-shot Veo-3 + random-play IDM | Hierarchical: WM planner + VLA | Zero-shot robot planning |
| [VLAW](https://arxiv.org/abs/2602.12063) | 2026 | Preprint (Stanford) | Iterative real->WM->synthetic->VLA loop | Co-improvement | +39.2% absolute |
| [VAMPO](https://arxiv.org/abs/2603.19370) | 2026 | Preprint | RL optimization of WM | Policy opt on video dynamics | Improved alignment |

### 6-LAM. Latent Action Models (Actions from Unlabeled Video)

| Paper | Year | Approach | Action Type | Key Finding |
|-------|------|----------|-------------|-------------|
| [Garrido et al.](https://arxiv.org/abs/2601.05230) | 2026 | Scale LAM to wild video | Continuous constrained | **VQ fails on diverse video** |
| [Olaf-World](https://arxiv.org/abs/2602.10102) | 2026 | REPA alignment objective | Latent anchored to effects | Better controllability |
| [AC-LAM](https://arxiv.org/abs/2604.03340) | 2026 | Additive composition | Compositional latent | Temporal composability |
| [HiLAM](https://arxiv.org/abs/2603.05815) | 2026 | Hierarchical skill discovery | Multi-level latent | Long-horizon skills |
| [FLAM](https://arxiv.org/abs/2602.16229) | 2026 | Factored scene decomposition | Per-factor latent | Multi-object handling |
| [JALA](https://arxiv.org/abs/2602.21736) | 2026 | Joint inverse dynamics alignment | Aligned embedding | Bridges latent <-> real |
| [World2Act](https://arxiv.org/abs/2603.10422) | 2026 | Post-training VLA alignment | WM-aligned actions | Policy transfer |

### 6-SYN. Synthetic Data / Sim-to-Real for Robotics

| Paper | Year | Pipeline Architecture | Key Numbers |
|-------|------|----------------------|-------------|
| [ComSim](https://arxiv.org/abs/2604.11386) | 2026 | Classical sim + neural sim hybrid | Closed-loop real-sim-real |
| [SIM1](https://arxiv.org/abs/2604.08544) | 2026 | Physics-aligned real-to-sim-to-real | 90% zero-shot, 1:15 ratio |
| [RoboCurate](https://arxiv.org/abs/2602.18742) | 2026 | Video gen + sim-replay verification | +70% to +179% improvement |
| [CRAFT](https://arxiv.org/abs/2604.03552) | 2026 | Video diffusion for bimanual data | Photorealistic demos |
| [EMMA](https://arxiv.org/abs/2509.22407) | 2025 | DreamTransfer DiT | +92% relative zero-shot |
| [InternData-A1](https://arxiv.org/abs/2511.16651) | 2025 | SAPIEN-based 630k trajectories | Matches real pretraining |
| [RoboTwin 2.0](https://arxiv.org/abs/2506.18088) | 2025 | Domain randomization (5 axes) | +367% relative improvement |

### 6-AGT. Agentic Data Collection for World Models

| Paper | Year | Agent Type | Autonomy Level | Data Quality Control |
|-------|------|-----------|---------------|---------------------|
| [PlayWorld](https://arxiv.org/abs/2603.09030) | 2026 | Physical robot self-play | Fully autonomous | Contact-rich diversity |
| [GameNGen](https://arxiv.org/abs/2408.14837) | 2024 | RL game agent | Fully autonomous | Exploration-driven |
| [Solaris](https://arxiv.org/abs/2602.22208) | 2026 | Multi-agent game bots | Automated | Synchronized multi-view |
| [RoboCurate](https://arxiv.org/abs/2602.18742) | 2026 | Sim-replay verifier | Semi-autonomous | Action-video consistency |
| [Action100M](https://arxiv.org/abs/2601.10592) | 2026 | VFM+LLM annotation agent | Fully autonomous | Multi-round Self-Refine |
| [Matrix-Game 3.0](https://arxiv.org/abs/2604.08995) | 2026 | Automated extraction bots | Fully autonomous | Industrial-scale QA |

### 6-DS. Large-Scale Video-Action Datasets

| Dataset | Year | Scale | Annotation Method | Key Innovation |
|---------|------|-------|-------------------|---------------|
| [Action100M](https://arxiv.org/abs/2601.10592) | 2026 | 100M+ segments | Fully automated (V-JEPA 2 + GPT-class) | Zero human annotation |
| Open X-Embodiment | 2023 | 22 robots, 527 skills | Multi-institution aggregation (RLDS) | Cross-embodiment standard |
| Bridge Data V2 | 2023 | 60K demos | Human VR teleoperation | Broad skill coverage |
| [Co-training Study](https://arxiv.org/abs/2602.01067) | 2026 | 4000 hr + 50M VL | Multi-modal (89 policies tested) | Discrete tokens = no benefit |
| [SPEAR-1](https://arxiv.org/abs/2511.17411) | 2025 | 45M frames (24 OXE) | 3D understanding | 20x demo reduction |

---

## 7. Embodied AI / Robotics Foundation Model Data Pipelines

### 7a. Robot Foundation Models (VLA / Policy Models)

| Paper | Year | Venue | Data Pipeline | Action Space | Scale |
|-------|------|-------|--------------|--------------|-------|
| [RT-1](https://arxiv.org/abs/2212.06817) | 2022 | RSS | Fleet teleoperation, RLDS | Tokenized discrete | 130K demos |
| [RT-2](https://arxiv.org/abs/2307.15818) | 2023 | preprint | VLM co-fine-tuning (PaLI-X) | Text tokens | Internet VL + robot |
| [RT-X / OXE](https://arxiv.org/abs/2310.08864) | 2023 | preprint | 22 robots, RLDS standardized | Heterogeneous | 800K traj |
| [Octo](https://arxiv.org/abs/2405.12213) | 2024 | preprint | Open X-Embodiment | Flexible tokenized | 800K traj |
| [OpenVLA](https://arxiv.org/abs/2406.09246) | 2024 | preprint | OXE -> VLM fine-tuning | 256-bin discretized | 970K traj |
| [pi0](https://arxiv.org/abs/2410.24164) | 2024 | RSS 2025 | Multi-platform teleop + VLM | Flow matching | Undisclosed |
| [RDT-1B](https://arxiv.org/abs/2410.07864) | 2024 | ICLR | Unified action space | Physically interpretable | 1.2B params |
| [GR00T N1](https://arxiv.org/abs/2503.14734) | 2025 | preprint | Real + human video + synthetic | Diffusion Transformer | Multi-source |
| [Magma](https://arxiv.org/abs/2502.13130) | 2025 | CVPR | SoM/ToM annotated heterogeneous | UI/robot actions | Mixed |
| [ABot-M0](https://arxiv.org/abs/2602.11236) | 2026 | preprint | UniACT curation, 6 datasets | Action Manifold Learning | 6M traj |
| [EO-1](https://arxiv.org/abs/2508.21112) | 2025 | preprint | EO-Data1.5M interleaved | AR + flow matching | 1.5M samples |
| [TRI LBM](https://arxiv.org/abs/2507.05331) | 2025 | preprint | Sim + real, Diffusion Policy | Diffusion-based | Multi-task |
| [DiffusionVLA](https://arxiv.org/abs/2412.03293) | 2024 | preprint | AR reasoning + diffusion | Diffusion | 2B-72B params |

### 7b. Data Collection Hardware & Systems

| System | Year | Cost | Key Innovation | Scale |
|--------|------|------|---------------|-------|
| [ALOHA](https://arxiv.org/abs/2304.13705) | 2023 | ~$20K | Bilateral teleop + ACT | 50 demos/task |
| [Mobile ALOHA](https://arxiv.org/abs/2401.02117) | 2024 | ~$32K | Mobile base + co-training | 50 demos/task |
| [UMI](https://arxiv.org/abs/2402.10329) | 2024 | ~$200 | Handheld + SLAM, hardware-agnostic | Unlimited |
| [DROID](https://arxiv.org/abs/2403.12945) | 2024 | ~$50K/site | Distributed, 564 scenes | 76K demos |

### 7c. Internet Video -> Robot Learning

| Paper | Year | Approach | Gap Bridge |
|-------|------|----------|------------|
| R3M | 2022 | Visual pre-training from Ego4D | Frozen features |
| VIP | 2022 | Value pre-training | Temporal distance reward |
| [UniPi](https://arxiv.org/abs/2302.00111) | 2023 | Video generation as policy | Inverse dynamics |
| [GR-1](https://arxiv.org/abs/2312.13139) | 2023 | Video generative pre-training | Joint video+action prediction |
| [VidBot](https://arxiv.org/abs/2503.07135) | 2025 | 3D affordance from human video | Depth+SfM |
| [LingBot-VA](https://arxiv.org/abs/2601.21998) | 2026 | Causal world modeling | MoT shared latent |

### 7d. VLM/LLM Data Augmentation for Robotics

| Paper | Year | Method | Output |
|-------|------|--------|--------|
| [ROSIE](https://arxiv.org/abs/2302.11550) | 2023 | Diffusion inpainting augmentation | Novel objects/backgrounds |
| [Interleave-VLA](https://arxiv.org/abs/2505.02152) | 2025 | Auto text->interleaved img-text | 210K episodes |
| [OWMM-Agent](https://arxiv.org/abs/2506.04217) | 2025 | Agentic VLM data synthesis | Mobile manipulation data |

### 7e. Simulation Data Generation for Robotics

| Framework | Year | Key Feature | Tasks |
|-----------|------|-------------|-------|
| [RoboCasa](https://arxiv.org/abs/2406.02523) | 2024 | GenAI assets + LLM tasks | 100 |
| ManiSkill 2/3 | 2023-24 | GPU-parallel sim | Diverse |
| LIBERO | 2023 | Lifelong learning benchmark | 130 |
| RLBench | 2020 | 100 tasks, auto-demos | 100 |

*Full survey: [embodied-ai-data-pipelines-survey.md](./embodied-ai-data-pipelines-survey.md)*

---

## 8. Image Generation Data Pipelines

| Paper / Resource | Year | Type | Key Contribution | Our Relevance |
|-----------------|------|------|-----------------|---------------|
| [LAION-5B](https://arxiv.org/abs/2210.08402) | 2022 | NeurIPS DB Track | 5.85B CLIP-filtered image-text pairs; aesthetic predictor; NSFW/watermark detection | Foundational dataset; filtering methodology |
| [DataComp](https://arxiv.org/abs/2304.14108) | 2023 | NeurIPS | 12.8B candidate pool; dataset curation as benchmark; DataComp-1B beats OpenAI CLIP | Dataset curation paradigm |
| [Data Filtering Networks](https://arxiv.org/abs/2309.17425) | 2023 | Preprint | Learned filtering beats heuristics; DFN-5B, 84.4% IN zero-shot | Filtering methodology |
| [T-MARS](https://arxiv.org/abs/2307.03132) | 2023 | Preprint | Circumvent text features for better image-text filtering | Filtering technique |
| [LAION-Aesthetics Audit](https://arxiv.org/abs/2601.09896) | 2026 | Preprint | Bias audit of LAION aesthetic predictor | Quality-awareness for filtering |
| [img2dataset](https://github.com/rom1504/img2dataset) | 2021+ | Open-source (4.4K stars) | Parallel download+resize+package; 100M images in 20h | Image pipeline tooling |

## 9. Video Datasets & Captioning at Scale

| Paper / Resource | Year | Type | Key Contribution | Our Relevance |
|-----------------|------|------|-----------------|---------------|
| WebVid-10M | 2021 | Preprint | 10M stock footage video-text pairs; noisy alt-text captions | Legacy dataset reference |
| HD-VILA-100M | 2022 | CVPR | 100M clips from 3.3M YouTube videos; ASR-based text | Source data for many pipelines |
| [InternVid](https://arxiv.org/abs/2307.06942) | 2023 | CVPR 2024 | 7M videos / 234M clips; multi-scale LLM captioning; ViCLIP | Key video dataset |
| [Panda-70M](https://arxiv.org/abs/2402.19479) | 2024 | CVPR 2024 | 70M clips; multi-teacher captioning + retrieval selection | Major video dataset |
| [ShareGPT4Video](https://arxiv.org/abs/2406.04325) | 2024 | Preprint | 40K GPT-4V gold + 4.8M via ShareCaptioner-Video; differential captioning | State-of-art captioning approach |
| [OpenVid-1M](https://arxiv.org/abs/2407.02371) | 2024 | Preprint | 1M precise high-quality pairs; 433K 1080p subset | Quality-focused video dataset |
| ViMix-14M | 2025 | Preprint | 14M curated multi-source video-text dataset | Recent large-scale dataset |
| Tiger200K | 2025 | Preprint | 200K manually curated high visual quality videos | Quality benchmark |

## 10. Video Generation Models (with Data Pipeline Documentation)

| Paper / Resource | Year | Type | Key Contribution | Our Relevance |
|-----------------|------|------|-----------------|---------------|
| [CogVideoX](https://arxiv.org/abs/2408.06072) | 2024 | ICLR 2025 | 3D VAE + expert transformer; video captioning model; progressive training | Pipeline reference |
| [Open-Sora Plan](https://arxiv.org/abs/2412.00131) | 2024 | Preprint (12.2K stars) | WF-VAE + Skiparse; multi-dimensional data curation pipeline | Primary pipeline reference |
| [Open-Sora (HPC-AI Tech)](https://github.com/hpcaitech/Open-Sora) | 2024 | Open-source (28.9K stars) | Most complete open data pipeline: scene detect, filter, caption | Implementation reference |
| [LTX-Video](https://github.com/Lightricks/LTX-Video) | 2024 | Open-source (10K stars) | Efficient video generation | Architecture reference |
| Kandinsky 5.0 | 2025 | Preprint | Foundation model for image & video with pipeline details | Recent system reference |

## 11. Video Data Pipeline Tools

| Tool | Stars | Scope | Key Capability |
|------|-------|-------|---------------|
| [video2dataset](https://github.com/iejMac/video2dataset) | 653 | Video download + packaging | Extends img2dataset to video; webdataset output |
| PySceneDetect | 3K+ | Scene boundary detection | ContentDetector + AdaptiveDetector |
| TransNetV2 | 1K+ | Scene boundary detection | Neural network-based; higher accuracy |
| webdataset | 2K+ | Data format | Tar-based streaming for large-scale training |

---

*Full survey on image/video data pipelines: [data-pipelines-survey.md](./data-pipelines-survey.md)*

---

## Our Comparison

*To be populated as experiments are conducted.*

| Our Approach | vs. Baseline | Metric | Result |
|-------------|-------------|--------|--------|
| TBD | TBD | TBD | TBD |
