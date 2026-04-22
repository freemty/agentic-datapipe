# Changelog

## v0.1.1 — 2026-04-22

### 变更
- landscape.md: 新增 DataEvolve (arXiv:2603.14420) 至 §1 Data Curation 和 §3 Agentic Pipeline Systems
- agentic-datapipe-survey.md: 新增 DataEvolve 条目至 §3 + 更新 section summary

### 其他
- 深读 LingBot-World (arXiv:2601.20540)，分析其三源数据引擎与三层标注体系对本项目的借鉴价值
- 讨论 DataEvolve evolutionary curation 迁移到可控视频生成的 design space（category 定义、strategy space、fitness approximation、16 GPU 约束下的实验路线）

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
