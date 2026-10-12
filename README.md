# research-swarm

**A multi-agent swarm pipeline that turns "a modality / an organ" into novelty-checked, ranked research proposals and executable experiment plans — built for medical imaging AI papers.**

Battle-tested through three full research rounds (breast → lung-nodule × breast → malignancy-prediction portfolio). Across those rounds the pipeline's built-in checks intercepted **8 data-fact errors, 1 citation hallucination, and 3 phantom datasets** — before any GPU time was spent.

[中文说明（README.zh-CN.md）](README.zh-CN.md)

## The pipeline

```
P0 goal (human) → P1 literature sweep → P2 dataset inventory (+ falsification)
  → P2.5 private-data interview (6 structured questions)
  → P3 idea generation (3 theme-cluster agents × 5 axes)
  → P4 three-expert scoring → [human: pick Top-N]
  → P5 per-proposal novelty check → [human: continue / pivot / downgrade]
  → P6 paper-grade proposal → P7 scoop-window & competitor recon
  → executable experiment plan (hand-off ready)
```

| Stage | Parallelism | Output | Human gate |
|---|---|---|---|
| P0 goal definition | — | scope, venues, constraints | fill in |
| P1 literature sweep | 2-4 | paper tables + exclusion list + "recipe" summary | — |
| P2 dataset inventory | 3-4 | dataset cards + **falsification list** + leakage-chain map | — |
| P2.5 private-data interview | human dialogue | private-data cards + attribute→value mapping | the interview |
| P3 idea generation | **3+ (theme clusters)** | idea catalog N≈12-16 | prune infeasible |
| P4 expert scoring | **always 3 personas** | ranked table (mean / consensus / disagreement) | **pick Top-N** |
| P5 novelty check | **1 per proposal** | neighbor table + 3 intercepted-risk lists | **continue / pivot / downgrade** |
| P6 proposal expansion | 1 per proposal | paper-grade plan (13 elements) | **commit decision** |
| P7 window & recon | 1-3 | scoop deadline + monthly monitoring list | deadline sign-off |

## Why a swarm, not one agent

- A single idea agent produces correlated ideas; three theme-cluster agents plus aggregation widen coverage.
- A single expert has systematic bias (one real case: clinical expert scored a proposal 4/10, methodologist scored its novelty 8/10) — the three-persona mean with explicit disagreement is far more trustworthy.
- Novelty checks are embarrassingly parallel: one self-contained agent per proposal, mechanically mergeable conclusions.

## The three iron rules

1. **Data-fact checking precedes mechanism design.** Claims must be bound to verified data fields; second-hand numbers are wrong until verified; citation hallucination is intolerable; phantom datasets get explicitly falsified.
2. **Parallel agent prompts must be self-contained.** Agents cannot see each other — paste context into every prompt; fix output schemas before fan-out; isolate writes (each agent owns its numbered file).
3. **Humans decide at aggregation gates.** Top-N selection, continue/pivot/downgrade after novelty checks, project commitment, deadline sign-off — agents exhaust the facts and options; these four decisions stay human.

## Highlights: the private-data interview (P2.5)

Privately-held data usually surfaces mid-project and reshapes the whole portfolio. P2.5 makes it a mandatory stage: six structured questions (holding / annotation / ground-truth tier / acquisition protocols / governance / overlap risk) plus an **attribute → research-value mapping** (pathology gold standard → external validation & audit; paired protocols → protocol-invariance experiments; prospective approval → prospective arms; enriched labels → label-shift laboratory …) and integration gates (external-validation by default; training requires justification + interlocks).

## Repository layout

```
SKILL.md                       # skill entry (frontmatter + pipeline + iron rules)
references/
  pipeline-prompts.md          # all stage prompts, P0-P7 + P2.5 ({{placeholders}})
  orchestration.md             # fan-out tables, shared-context block, aggregator prompt, minimal plan
  pitfalls.md                  # orchestration discipline & hard-won pitfalls
templates/
  proposal-template.md         # 13-element paper-grade proposal skeleton
  experiment-plan-template.md  # hand-off execution plan for a training team
  scoring-template.md          # three-persona scoring (rubric + schema + aggregation)
  novelty-check-template.md    # channel log / neighbor table / verdicts / risk lists
  kickoff-template.md          # executor kick-off instruction
examples/
  case-structure.md            # minimal 3-document structure of a real project (desanitized)
```

## Quickstart

- **As a skill**: clone into your agent's skills directory; the SKILL.md frontmatter triggers on 找课题 / 调研 / 查新 / 实验计划 / novelty check / dataset inventory, etc.
- **As a playbook**: fill P0, then follow the minimal orchestration plan in `references/orchestration.md` §8.5 — four parallel batches (4 + 3 + 3 + 5 agents) and four human gates, ≤30 min each.

## License

[MIT](LICENSE)
