# agentic-datapipe

面向视频/世界模型训练数据的自主进化式数据管线 —— 将进化策略搜索应用于可控视频生成的数据构建。

## 问题

训练可控视频生成模型（LTX、LingBot-World、Matrix-Game 等）需要高质量的 action-conditioned 视频数据：
- 精确标注相机轨迹和控制信号
- 经过视觉质量、时序一致性、控制信号清晰度的多维过滤
- 按内容类型、运动模式、控制类型进行分类

当前的数据管线是人工设计的一次性流程。没有任何现有工具能同时实现：大规模互联网视频 + 精确动作标注 + 通用域覆盖 + 迭代质量精炼。

## 方法

将 [DataEvolve](https://arxiv.org/abs/2603.14420) 的进化策略设计扩展到视频数据 curation：

```
观察数据 → 设计策略 → 执行 curation → 评估 fitness → 精炼策略
   ↑                                                      |
   └──────────────────────────────────────────────────────┘
```

四个设计轴：
1. **类别定义** — 按运动模式 x 控制信号类型划分视频
2. **策略空间** — 时序分割、质量过滤、标注策略、控制信号提取/过滤
3. **Fitness 近似** — VLM-as-judge + 控制精度指标 + 周期性小模型验证
4. **进化机制** — 跨代知识积累的迭代精炼

## 项目结构

```
docs/
  papers/          # 文献调研与 landscape
    landscape.md   # 文献总图（7 大板块，100+ 论文）
  design/          # 设计文档
exp/               # 实验追踪
scripts/           # 实验编排
viewer/            # 结果查看器
```

## 文档

| 文档 | 说明 |
|------|------|
| [文献 Landscape](docs/papers/landscape.md) | 领域文献地图：数据 curation、世界模型、视频生成管线 |
| [进化式视频 Curation 设计](docs/design/evolutionary-video-curation.md) | Design space：4 个设计轴、16 GPU 可行性方案、关键 ablation |
| [视频管线工具调研](docs/design/video-pipeline-tools.md) | 11 个开源工具调研（Cosmos-Curate、video2dataset 等） |
| [CHANGELOG](CHANGELOG.md) | 版本记录 |

## 关键参考

- [DataEvolve](https://arxiv.org/abs/2603.14420) — 自主进化策略设计，用于数据 curation
- [LingBot-World](https://arxiv.org/abs/2601.20540) — 三源数据引擎 + 三层分级标注
- [Matrix-Game 2.0](https://arxiv.org/abs/2508.13009) — 最精确的动作标注管线（毫秒级同步）
- [HY-GameCraft-2](https://arxiv.org/abs/2511.23429) — 双标注策略（标准描述 + 交互差异描述）
- [Yume](https://arxiv.org/abs/2507.17744) — QCM 相机量化；数据/代码/权重全开源
- [Cosmos WFM](https://arxiv.org/abs/2501.03575) — 最大规模管线（2000 万小时原始视频）

## 开发环境

本项目使用 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 作为主要开发工具，配合以下插件和 skills。

### Claude Code 插件

通过 `/install-plugin` 安装（project scope）：

| 插件 | Registry | 说明 |
|------|----------|------|
| [labmate](https://github.com/freemty/labmate) | `labmate-marketplace` | 研究实验管理框架：实验编排、分析、文献阅读、slides 生成 |
| [superpowers](https://github.com/anthropics/claude-plugins-official) | `claude-plugins-official` | Skills 系统增强：brainstorming、code review、debugging 等 |

### 自定义 Skills（yuanbo-skills）

```bash
git clone git@github.com:freemty/yuanbo-skills.git ~/code/projects/yuanbo-skills
```

创建 symlink 到 `~/.claude/skills/`：

```bash
# 核心 skills
ln -s ~/code/projects/yuanbo-skills/skills/web-fetcher ~/.claude/skills/web-fetcher
ln -s ~/code/projects/yuanbo-skills/skills/paper-storyteller ~/.claude/skills/paper-storyteller
ln -s ~/code/projects/yuanbo-skills/skills/paper-style ~/.claude/skills/paper-style
ln -s ~/code/projects/yuanbo-skills/skills/weekly-report ~/.claude/skills/weekly-report
ln -s ~/code/projects/yuanbo-skills/skills/cc-navigator ~/.claude/skills/cc-navigator
ln -s ~/code/projects/yuanbo-skills/skills/beamer-style ~/.claude/skills/beamer-style

# plugins (作为 skills 安装)
ln -s ~/code/projects/yuanbo-skills/plugins/paper-review ~/.claude/skills/paper-review
ln -s ~/code/projects/yuanbo-skills/plugins/unbox-skills/unbox ~/.claude/skills/unbox
ln -s ~/code/projects/yuanbo-skills/plugins/unbox-skills/unbox-graph ~/.claude/skills/unbox-graph
ln -s ~/code/projects/yuanbo-skills/plugins/unbox-skills/unbox-to-wiki ~/.claude/skills/unbox-to-wiki
```

### 关键能力

| 功能 | 来源 | 用法 |
|------|------|------|
| 实验管理 | labmate | `/labmate:new-experiment`, `/labmate:analyze-experiment` |
| 文献深读 | labmate | `/labmate:read-paper <url>` |
| 网页抓取 | yuanbo-skills/web-fetcher | 自动路由：arXiv、YouTube、GitHub 等 |
| 论文写作辅助 | yuanbo-skills/paper-style | 学术写作风格检查 |
| 周报生成 | yuanbo-skills/weekly-report | 自动汇总周进展 |

## 状态

早期研究阶段。文献调研和 design space 探索已完成，尚未启动实验。

## License

TBD
