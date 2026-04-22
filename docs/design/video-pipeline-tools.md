# Video Data Processing/Curation Pipeline -- 开源工具调研

> 调研日期: 2026-04-22
> 目的: 为 video generation / world model 训练数据构建选型

---

## 1. 快速对比表

| 工具 | 组织 | Stars | 定位 | 视频原生 | GPU加速 | LLM/VLM集成 | 分布式 | 最后活跃 |
|------|------|-------|------|----------|---------|-------------|--------|----------|
| **Cosmos-Curate** | NVIDIA | ~178 | 端到端视频 curation | +++++ | NVIDIA GPU (PyNvVideoCodec) | Qwen2-VL captioning | Ray 集群 | 2026-03 (v1.2.2) |
| **video2dataset** | iejMac / DataToML | ~2k | 视频下载+打包 | ++++ | CPU-only | 无 | Spark/Slurm/MP | 2024 (维护中) |
| **Open-Sora** (数据管线) | HPC-AI Tech | ~23k | video gen + 内置数据处理 | ++++ | 部分 | PLLaVA/LLaVA captioning | 脚本级 | 2025-03 (v2.0) |
| **Open-Sora-Plan** (数据管线) | PKU-YuanGroup | ~12.2k | video gen + 多维 curation | ++++ | 部分 | ShareGPT4Video | 脚本级 | 2026-03 (v1.5) |
| **CogVideo** (tools/) | THUDM/zai-org | ~12.7k | video gen + captioning 工具 | +++ | 部分 | CogVLM2-Caption | 脚本级 | 2025-03 |
| **NeMo-Curator** | NVIDIA | ~1.5k | 可扩展 multi-modal curation | ++ (主力文本) | GPU (cuDF/RAPIDS) | 分类器集成 | Dask/RAPIDS | 2026 (活跃) |
| **DataTrove** | Hugging Face | ~2.5k | 大规模文本处理框架 | - (文本only) | CPU | LLM synthetic gen | Local/Slurm/Ray | 2026 (活跃) |
| **distilabel** | argilla-io | ~3.2k | 合成数据 + AI feedback | - (文本为主) | CPU | 多LLM provider | Ray | 2025-12 (社区维护) |
| **img2dataset** | rom1504 / DataToML | ~3.5k | 图像下载+打包 | - (图像only) | CPU | 无 | Spark/Slurm | 2024 (稳定) |
| **LiteGen** | Vchitect | ~100 | DiT 训练加速框架 | - (非数据管线) | GPU | 无 | DDP/ZeRO/SP | 2025 |
| **HunyuanVideo** | Tencent | ~8k | video gen 模型 | +++ (内部管线) | GPU | Prompt Rewrite | 内部 | 2025-11 (v1.5) |

> 说明: 视频原生列 `+` 越多表示对视频数据管线覆盖越完整; `-` 表示该工具不直接处理视频

---

## 2. 各工具详细分析

### 2.1 NVIDIA Cosmos-Curate

**GitHub**: https://github.com/nvidia-cosmos/cosmos-curate
**Stars**: 178 | **Forks**: 28 | **Contributors**: 15 | **License**: Apache-2.0
**最新版本**: v1.2.2 (2026-03-25) | **Commits**: 391

#### 核心定位
Cosmos-Curate 是 NVIDIA Cosmos 项目的训练数据生成引擎,专为大规模视频 curation 设计。它是目前开源领域**最完整的端到端视频 curation 系统**。

#### 管线覆盖阶段
| 阶段 | 支持 | 说明 |
|------|------|------|
| 视频分割 (Splitting) | Y | 场景检测 + 时间切片 |
| 标注 (Annotation) | Y | VLM-based captioning (Qwen2-VL 等) |
| 过滤 (Filtering) | Y | 多维质量过滤 |
| 去重 (Deduplication) | Y | GPU 加速嵌入去重 (cuML) |
| 数据集生成 (Packaging) | Y | 输出格式化 |
| 下载 | N | 不直接处理下载 (假定已有原始视频) |

#### 关键能力
- **GPU 加速流水线**: 基于 Cosmos-Xenna 框架, 底层 Ray 分布式调度, PyNvVideoCodec 硬件解码
- **VLM captioning**: 集成 Qwen2-VL 等多模型家族做视频描述
- **模块化管线架构**: `cosmos_curate/pipelines/video/` 下有多个 reference pipeline
- **AV (自动驾驶) 管线**: 支持多摄像头视频、GPS + LiDAR 处理 (upcoming)
- **云端部署**: 支持 Kubernetes (Helm charts), NVIDIA Cloud Functions, Slurm
- **可观测性**: 内置监控 dashboard

#### 规模与吞吐
- 为 Cosmos 世界模型训练服务, 处理过 PB 级视频数据
- Ray 集群可水平扩展到数百 GPU 节点
- GPU 解码显著提升吞吐 (相比 CPU-only 方案)

#### 局限
- 依赖 NVIDIA GPU 生态 (PyNvVideoCodec, cuML, RAPIDS)
- 社区较小 (178 stars), 文档主要面向 NVIDIA 内部用户
- 不含下载阶段, 需配合 video2dataset 或自建下载器

---

### 2.2 video2dataset

**GitHub**: https://github.com/iejMac/video2dataset
**Stars**: ~2k | **License**: MIT
**最新版本**: PyPI 有发布 | 维护者: iejMac, Romain Beaumont 等

#### 核心定位
视频领域的 img2dataset -- 从 URL 列表批量下载和打包视频数据集。社区标准的视频下载工具。

#### 管线覆盖阶段
| 阶段 | 支持 | 说明 |
|------|------|------|
| 下载 (Download) | Y | yt-dlp 支持的所有站点 |
| 裁剪/切割 (Clipping) | Y | 按时间戳切割, 场景检测切割 |
| 降采样 (Resize/Downsample) | Y | FPS 降采样, 分辨率调整 |
| 光流计算 (Optical Flow) | Y | 可计算并存储光流 metadata |
| 打包 (Output Format) | Y | WebDataset / Parquet / TFRecord / Files |
| Captioning | N | 无内置, 但可通过 re-processing 链式调用外部工具 |
| 过滤 | N | 需用户自定义 |
| 去重 | N | 不内置 |

#### 关键能力
- **高吞吐下载**: 10M 视频 / 12 小时 (16 核机器)
- **链式处理**: WebDataset 作为输入格式支持多轮 re-processing
- **分布式**: multiprocessing / PySpark / Slurm
- **fsspec 文件系统**: 支持 S3, GCS, HDFS 等
- **增量模式**: 中断后可续传
- **W&B 集成**: 监控下载进度和错误

#### 吞吐基准
- WebVid 10M: 12h (16 cores)
- YouTube 视频明显慢于直链 mp4

#### 局限
- CPU-only, 无 GPU 加速
- 不含质量过滤、captioning 等 AI 环节
- 作为管线入口 (下载层) 很好, 需要下游配合其他工具

---

### 2.3 Open-Sora 数据管线

**GitHub**: https://github.com/hpcaitech/Open-Sora
**Stars**: ~23k | **License**: Apache-2.0
**最新版本**: v2.0 (2025-03)

#### 核心定位
Open-Sora 是完整的 video generation 项目, 其数据处理管线在 v1.1 report 中详细描述。

#### 数据处理覆盖
根据 Tech Report, 其数据管线包含:
1. **视频收集**: 从多源爬取
2. **场景分割**: 基于 PySceneDetect 的场景检测
3. **Filter Cascading**:
   - 美学分数过滤
   - 光流 / 运动量分析
   - OCR 文字检测过滤
   - 图像质量评分
4. **Video Captioning**: PLLaVA / LLaVA (图像 caption) + 自定义 video captioner
5. **Motion Score**: 训练时注入 motion score 条件

#### 关键能力
- **端到端**: 从数据处理到训练到推理的完整方案
- **Motion Score**: 运动评分作为可控生成条件, 非常独特
- **Prompt Refine**: ChatGPT-based prompt 优化
- **ColossalAI 加速**: 序列并行推理

#### 局限
- 数据处理脚本散落在 `scripts/` 中, 非独立可复用的库
- 缺乏通用管线抽象, 紧耦合于 Open-Sora 训练 pipeline
- 不支持任意数据集, 主要服务于自身训练

---

### 2.4 Open-Sora-Plan 数据管线

**GitHub**: https://github.com/PKU-YuanGroup/Open-Sora-Plan
**Stars**: ~12.2k | **License**: MIT
**最新版本**: v1.5.0 (2025-06, mindspeed_mmdit branch)

#### 核心定位
北大-兔展 AIGC 联合实验室, v1.3 起引入系统性的数据过滤策略。

#### 数据处理覆盖 (v1.3+)
1. **WFVAE**: 高压缩率 Wavelet Flow VAE
2. **Prompt Refiner**: 用 LLM 改写用户 prompt
3. **数据过滤策略**: 多维度 curation
   - 美学打分
   - 运动平滑度
   - 文本遮挡检测
   - 分辨率/时长筛选
4. **Sparse Attention + Bucket Training**: 数据排列优化

#### 关键能力
- **v1.5 在华为昇腾上完全训练**, 提供非 NVIDIA 路线
- **SUV (sparse DiT)**: 数据管线与模型架构紧密配合
- **ShareGPT4Video** 标注: 长视频描述

#### 局限
- 数据管线与训练代码紧耦合
- 文档和代码分散在多个 branch 中
- 非独立可复用的管线工具

---

### 2.5 CogVideo / CogVideoX

**GitHub**: https://github.com/THUDM/CogVideo (已迁移至 zai-org/CogVideo)
**Stars**: ~12.7k | **License**: Apache-2.0

#### 数据处理工具
- **CogVLM2-Caption**: 专为 CogVideoX 训练过程设计的 video-to-text caption 模型
  - 2024-09 开源, HuggingFace 可下载
  - 将视频数据转换为文本描述
- **tools/ 目录**: 包含数据处理辅助脚本
- **CogKit**: fine-tuning 和推理框架 (2025-03)

#### 关键能力
- **3D Causal VAE**: 几乎无损视频重建
- **Video Captioning 专用模型**: CogVLM2-Caption 可独立使用
- **DDIM Inverse**: 支持视频编辑 pipeline

#### 局限
- 没有完整的数据 curation pipeline
- CogVLM2-Caption 仅覆盖 captioning 一个环节
- tools/ 中的脚本不构成可复用框架

---

### 2.6 NVIDIA NeMo-Curator

**GitHub**: https://github.com/NVIDIA/NeMo-Curator
**Stars**: ~1.5k | **Forks**: 259 | **License**: Apache-2.0

#### 核心定位
可扩展的数据预处理和 curation 工具包, 原生支持文本, 正在扩展多模态。

#### 管线覆盖
- **文本 curation**: 完整覆盖 (下载 -> 提取 -> 去重 -> 过滤 -> 分类)
- **GPU 加速**: 基于 RAPIDS/cuDF/Dask, 全面 GPU 加速
- **多模态支持**: 正在添加 image/video curation (截至 2026 仍在发展中)
- **去重**: MinHash, Exact Dedup, Semantic Dedup (GPU 加速)
- **分类器**: 支持 domain/quality/safety 分类
- **合成数据**: LLM 集成合成数据生成

#### 关键能力
- **工业级扩展性**: Dask 分布式, 可处理 trillion-token 级数据
- **GPU 原生**: RAPIDS 生态的核心优势
- **Synthetic Data Generation**: 可用于生成训练数据
- **Quality Scoring**: 多种质量评估器

#### 局限
- **视频支持尚不完善**: 当前主要面向文本/文档 curation
- 视频特定功能 (场景检测, 运动分析等) 不在当前版本中
- 与 Cosmos-Curate 定位不同: NeMo-Curator 是通用 curation, Cosmos-Curate 是视频专用

---

### 2.7 Hugging Face DataTrove

**GitHub**: https://github.com/huggingface/datatrove
**Stars**: ~2.5k | **License**: Apache-2.0

#### 核心定位
大规模文本数据处理框架, FineWeb 数据集的制作工具。**不直接支持视频**。

#### 为什么仍值得关注
- **管线抽象优秀**: Reader -> Filter -> Dedup -> Writer 的模块化设计
- **Executor 抽象**: Local / Slurm / Ray 执行器, 平台无关
- **去重能力**: MinHash, Sentence Dedup, ExactSubstr
- **Synthetic Data**: 支持 LLM inference pipeline 生成合成数据
- **参考架构**: 其 pipeline 设计可作为视频管线的参考

#### 局限
- 完全面向文本, 无视频处理能力
- Document 抽象仅含 text/id/metadata, 不含多媒体

---

### 2.8 distilabel

**GitHub**: https://github.com/argilla-io/distilabel
**Stars**: ~3.2k | **License**: Apache-2.0
**状态**: 原作者已离开, 社区维护 (2025-12 last commit)

#### 核心定位
AI feedback + 合成数据生成框架。面向 LLM, 非视频。

#### 与我们用例的关联
- **Synthetic caption generation**: 可用于生成视频描述的合成改进
- **ImageGeneration task**: 近期增加了图像生成任务支持
- **多LLM provider**: 统一 API 调用多家 LLM
- **Ray 分布式**: 可扩展

#### 局限
- 不处理视频数据
- 社区维护状态, 未来发展不确定

---

### 2.9 img2dataset

**GitHub**: https://github.com/rom1504/img2dataset
**Stars**: ~3.5k | **License**: MIT

#### 核心定位
video2dataset 的前身/姊妹项目, 面向图像。100M URL / 20h (单机)。

#### 与我们用例的关联
- **架构参考**: video2dataset 完全继承了其设计模式
- **图像预训练数据**: 如果做 image-video joint training, 需要图像数据

---

### 2.10 HunyuanVideo (参考)

**GitHub**: https://github.com/Tencent/HunyuanVideo
**Stars**: ~8k | **License**: Tencent Hunyuan Community License

#### 数据处理相关
- **Prompt Rewrite Model**: 开源了 prompt 改写模型 (基于 Hunyuan-Large fine-tune)
  - Normal mode: 增强模型理解用户意图
  - Master mode: 增强构图、光照、镜头运动描述
- **Data Curation** (论文中描述): "data curation, image-video joint model training"
  - 具体 curation 代码**未开源**

#### 关键价值
- Prompt Rewrite Model 可独立用于任何 video gen 管线的 prompt 优化
- 论文中的 data curation 策略值得参考

---

## 3. 管线阶段覆盖矩阵

```
                    下载  分割  过滤  Captioning  去重  打包  运动分析  Camera Pose
Cosmos-Curate       -     Y    Y     Y           Y    Y      -        -
video2dataset       Y     Y    -     -           -    Y      Y(光流)   -
Open-Sora           -     Y    Y     Y           -    -      Y        -
Open-Sora-Plan      -     Y    Y     Y           -    -      部分      -
CogVideo            -     -    -     Y           -    -      -        -
NeMo-Curator        Y*    -    Y     -           Y    Y      -        -
DataTrove           Y*    -    Y     -           Y    Y      -        -

* NeMo-Curator/DataTrove 的下载主要面向文本数据 (Common Crawl 等)
```

---

## 4. 架构与设计模式对比

### 4.1 管线框架层次

```
Level 3 - 端到端系统:     Cosmos-Curate (视频), Open-Sora (训练)
Level 2 - 通用框架:        DataTrove (文本), NeMo-Curator (文本+)
Level 1 - 单功能工具:      video2dataset (下载), CogVLM2-Caption (标注)
Level 0 - 脚本集合:        Open-Sora scripts, Open-Sora-Plan scripts
```

### 4.2 分布式执行模型

| 工具 | 调度器 | 适用规模 |
|------|--------|----------|
| Cosmos-Curate | Ray (Cosmos-Xenna) | 100+ GPU 节点 |
| NeMo-Curator | Dask + RAPIDS | 数十节点 GPU |
| DataTrove | Local/Slurm/Ray | 数百 CPU 节点 |
| video2dataset | MP/Spark/Slurm | 数十节点 CPU |
| Open-Sora* | 脚本级 | 单机/少量节点 |

### 4.3 视频处理技术栈

| 工具 | 解码器 | 场景检测 | 质量评估 |
|------|--------|----------|----------|
| Cosmos-Curate | PyNvVideoCodec (GPU) | 内置 | AI 模型 |
| video2dataset | ffmpeg/decord (CPU) | PySceneDetect | 无 |
| Open-Sora | decord | PySceneDetect | 美学评分器 |
| Open-Sora-Plan | decord | 自定义 | 多维评分 |

---

## 5. Gap 分析: 现有工具对我们用例的缺失

我们的目标: **Evolutionary video curation for controllable generation** -- 通过迭代式数据精炼, 为可控视频生成 (camera control, action control, physics-aware) 构建高质量训练数据。

### 5.1 缺失能力

#### (A) Camera Pose / 3D 几何信息提取
- **现状**: 无一工具原生支持 camera pose estimation (如 COLMAP, DUSt3R)
- **需求**: 可控生成需要 camera trajectory 标注
- **方案**: 需自建 stage, 集成 DUSt3R / MASt3R 等

#### (B) 动作/物理属性标注
- **现状**: 仅 Open-Sora 有 motion score, 但非结构化动作标注
- **需求**: 物体运动轨迹、物理合理性评分、action label
- **方案**: 需集成视频理解模型 (如 VideoMAE, InternVideo) 做结构化标注

#### (C) 时序一致性评估
- **现状**: 过滤主要基于单帧质量, 缺乏跨帧一致性评估
- **需求**: 闪烁检测、物体永恒性检查、运动连贯性评分
- **方案**: 需自建 temporal consistency checker

#### (D) 迭代式 / Evolutionary Curation
- **现状**: 所有工具都是单次 pass-through 管线
- **需求**: 基于模型训练反馈的迭代数据精炼 (train -> evaluate -> re-curate)
- **方案**: 这是我们项目的核心创新点, 需要自建 orchestration 层

#### (E) Agent-driven 数据决策
- **现状**: 过滤规则都是硬编码阈值
- **需求**: LLM agent 根据数据分布和模型表现动态调整 curation 策略
- **方案**: 需构建 agentic curation loop

#### (F) 统一的视频 + 3D + Action 数据格式
- **现状**: 各工具使用不同的 metadata schema
- **需求**: 统一描述 video + camera + action + physics 的数据格式
- **方案**: 需设计自己的 data schema

### 5.2 可复用的现有组件

| 我们需要的 | 最佳现有工具 | 集成难度 |
|-----------|-------------|----------|
| 视频下载 | video2dataset | 低 (pip install) |
| 场景分割 | Cosmos-Curate 或 PySceneDetect | 中 |
| 质量过滤 | Cosmos-Curate pipeline stages | 高 (需 NVIDIA GPU) |
| Video Captioning | CogVLM2-Caption / Cosmos-Curate (Qwen2-VL) | 中 |
| 去重 | NeMo-Curator (GPU MinHash) 或 Cosmos-Curate | 中 |
| Prompt 优化 | HunyuanVideo Prompt Rewrite | 低 |
| 管线框架 | DataTrove (设计参考) + Ray (执行) | 中 |
| 合成 caption | distilabel | 低 |

### 5.3 建议架构

```
Layer 4: Agentic Orchestration (我们的创新)
    |
    +-- Agent: 分析模型表现 -> 调整 curation 策略 -> 触发 re-curation
    |
Layer 3: Pipeline Stages (组合现有 + 自建)
    |
    +-- 下载: video2dataset
    +-- 分割: PySceneDetect / Cosmos-Curate
    +-- 过滤: Cosmos-Curate stages + 自建 (camera, physics)
    +-- 标注: CogVLM2-Caption + 自建 (camera pose, action)
    +-- 去重: NeMo-Curator GPU dedup
    +-- 打包: WebDataset format
    |
Layer 2: Execution Framework
    |
    +-- Ray (参考 Cosmos-Xenna) 作为分布式调度
    +-- GPU worker pool + CPU worker pool
    |
Layer 1: Storage & Schema
    |
    +-- 统一 metadata schema (video + camera + action + quality)
    +-- WebDataset / Parquet 存储
```

---

## 6. 结论

### 核心发现

1. **Cosmos-Curate 是视频 curation 的标杆**, 但社区小、依赖重, 适合参考架构而非直接使用
2. **video2dataset 是事实标准的下载层**, 直接使用即可
3. **Open-Sora/Plan/CogVideo 的数据脚本有价值**, 但非独立工具, 需要提取复用
4. **DataTrove 的管线抽象最优雅**, 值得参考其 Reader/Filter/Writer 模式
5. **NeMo-Curator 的 GPU 去重能力**可独立调用
6. **视频领域缺乏 "DataTrove for Video"** -- 一个通用、模块化、社区驱动的视频 curation 框架

### 我们的机会

现有工具没有覆盖的核心差异化:
- Camera pose estimation 集成到 curation pipeline
- Action/physics-aware 数据标注
- Evolutionary / agent-driven 迭代 curation
- Train-evaluate-curate closed loop

这些正是 agentic-datapipe 项目的切入点。

---

## 附录: 信息获取时间

所有 GitHub 数据获取于 2026-04-22, stars/commit 数据可能随时间变化。
