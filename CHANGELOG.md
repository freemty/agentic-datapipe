# Changelog

## v0.2.0 — 2026-04-22

### 新增
- docs/design/evolutionary-video-curation.md: Design doc — DataEvolve → 可控视频生成的 design space（4 设计轴 + 16 GPU 三阶段计划 + 关键 ablation）
- docs/design/video-pipeline-tools.md: 开源视频数据处理工具调研（11 个工具，含 Cosmos-Curate, video2dataset, Open-Sora 等）
- docs/papers/interactive-world-models-survey.md: Interactive world model 技术报告调研（7 篇论文：Cosmos WFM, GameGen-X, Matrix-Game v1/2.0, Yume, HY-GameCraft-2, LingBot-World）

### 变更
- landscape.md §6-WM: 新增 7 个 interactive world model 条目（含数据管线细节）
- landscape.md §1/§3: 新增 DataEvolve (arXiv:2603.14420)
- agentic-datapipe-survey.md §3: 新增 DataEvolve 条目 + 更新 summary

### 其他
- 深读 LingBot-World (arXiv:2601.20540)：三源数据引擎 + 三层标注体系 + 28B MoE 架构
- 深读 DataEvolve (arXiv:2603.14420)：进化式策略设计，cleaning > transformation
- 分析现有工具 gap：无一工具覆盖 camera pose 集成 / action-aware 标注 / evolutionary curation

## v0.1.0 — 2026-04-15

### 新增
- 项目骨架初始化（LabMate）：exp/, docs/, scripts/, viewer/, slides/
- 5 份领域 survey 文档（docs/papers/）：LLM/VLM 数据管线、图像/视频生成管线、World Model & Action、Agentic 自主数据系统、Embodied AI 机器人数据管线
- 文献 landscape 地图（docs/papers/landscape.md）
- 实验编排脚本（scripts/launch_exp.py, monitor_exp.sh, download_results.sh）
- 实验查看器（viewer/app.py + static/index.html）
- 项目知识 skill（.claude/skills/project-skill/SKILL.md）

### 构建与工具链
- git 仓库初始化
- .gitignore 配置（labmate 规则）
- CLAUDE.md 项目文档索引
- .pipeline-state.json 管线状态追踪
