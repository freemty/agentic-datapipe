# agentic-datapipe

> Agentic data pipeline for video/world model → world action model training data

## Quick commands

| Command | Purpose |
|---------|---------|
| /labmate:new-experiment | Scaffold new experiment |
| /labmate:analyze-experiment | Analyze results |
| /labmate:update-project-skill | Refresh project knowledge |
| python scripts/launch_exp.py --exp <id> | Launch experiment |

## Session startup

| What to do | Read first |
|-----------|-----------|
| Catch up on progress | .claude/skills/project-skill/SKILL.md |
| Check domain literature | docs/papers/landscape.md |
| Run current experiment | exp/{current_exp}/README.md |

## Project knowledge

- **Skill hub:** .claude/skills/project-skill/SKILL.md
- **Experiment log:** exp/summary.md
- **Domain papers:** docs/papers/

## Knowhow

- `docs/knowhow/infrastructure/` — Servers, networking, disk, GPU issues
- `docs/knowhow/toolchain/` — CLI tools, docker, conda/pip, framework tips
- `docs/knowhow/debug-solutions/` — Error investigation paths and fixes
- `docs/knowhow/runbooks/` — Step-by-step operational procedures

## Agents

| Agent | Model | Purpose |
|-------|-------|---------|
| @project-advisor | opus | Experiment history, findings, codebase navigation |
| @cc-advisor | sonnet | Claude Code workflow best practices |
| @domain-expert | opus | Reads papers, interprets experiment results |
| @exp-manager | sonnet | Monitors experiments, diagnoses failures |
| @slides-maker | sonnet | Generates HTML slides from analysis |
| @viz-frontend | sonnet | Builds analysis dashboards |
| @template-presenter | sonnet | Project overview and onboarding |

## Skills

All plugin skills use the `labmate:` prefix.

| Skill | Trigger |
|-------|---------|
| /labmate:new-experiment | Starting a new experiment |
| /labmate:analyze-experiment | After experiment completes |
| /labmate:update-project-skill | After major findings or when stale |
| /labmate:present-template | Generate overview slides |
| /labmate:weekly-progress | Summarize week's progress |
| /labmate:commit-changelog | Commit with CHANGELOG |

## Workflow

```
/labmate:new-experiment → run → /labmate:analyze-experiment
  → commit findings → /labmate:update-project-skill → repeat
```

Pipeline state tracked in .pipeline-state.json.

## Research principles

1. **Measure first** — attack the actual bottleneck, not your intuition
2. **Baselines are sacred** — every claim needs a reproducible baseline comparison
3. **Statistical rigor** — single-run results are anecdotal, track variance
4. **Ablation-driven** — multi-factor changes require per-factor isolation
5. **Respect negative results** — don't retry failed directions without new evidence
6. **Predict first** — record expected numbers before running, calibrate after

## Conventions

- **Exp naming:** exp{NN}{x} — number=major direction, letter=variant
- **Prompt versioning:** prompts/{component}/_v{NN}.md — never overwrite, always increment
- **CHANGELOG rule:** all iterating artifacts (prompts, skills, agents) must have CHANGELOG entries
- **Worktree rule:** destructive or exploratory changes use git worktree

## Current state

- **current_exp:** null
- **stage:** dev
- **skill_updated_at:** 2026-04-15

## Documentation index

| Path | Description |
|------|-------------|
| docs/papers/landscape.md | Domain literature landscape map |
| docs/papers/agentic-datapipe-survey.md | Agentic autonomous data systems survey |
| docs/papers/automated-data-pipelines-survey.md | LLM/VLM automated data pipeline survey |
| docs/papers/data-pipelines-survey.md | Image/video generation data pipeline survey |
| docs/papers/world-model-data-pipeline-survey.md | World model & action data pipeline survey |
| docs/papers/embodied-ai-data-pipelines-survey.md | Embodied AI & robotics data pipeline survey |
| exp/summary.md | Cross-experiment flight recorder |
