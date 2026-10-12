---
name: research-swarm
description: Research topic discovery and experiment planning pipeline for medical imaging AI papers, executed by multi-agent swarms. Use when the user asks to survey literature for a modality/organ/task, inventory public datasets, generate research ideas, score/rank proposals with multiple expert personas, run novelty or scoop checks, expand a proposal into a paper-grade plan, or produce an executable experiment plan for a training team. Trigger words: 找课题、开题、调研、文献盘点、数据集盘点、评分排序、查新、实验计划、研究方案.
---

# research-swarm — 课题发现与实验规划蜂群

一套经过三轮完整实践验证的流水线：把"某个模态/器官"变成"已查新、已排序、可开工的实验计划"。
全程多智能体蜂群执行（阶段间串行、阶段内扇出），人在 4 个聚合点做裁决。

## 何时使用

- "帮我找 X 方向能做的课题" / "调研 X 模态的公开数据集"
- "对这几个思路评分排序" / "查一下这个想法有没有人做过"
- "把这个思路写成实验计划/研究方案"

## 流水线总览

```
P0 目标定义(人工) → P1 文献检索 → P2 数据集盘点(含证伪) → P3 思路生成(3簇)
  → P4 三专家评分 → [人工:选TopN] → P5 逐案查重 → [人工:继续/转向/降级]
  → P6 方案展开 → P7 窗口与竞对侦察 → 实验计划(交接执行版)
```

| 阶段 | 提示词位置 | 并行度 | 产出物 | 人工门 |
|---|---|---|---|---|
| P0 | `references/pipeline-prompts.md` §P0 | — | 目标定义 | 填写 |
| P1 | 同上 §P1 | 2-4 | 检索详析表+排除清单+配方归纳 | — |
| P2 | 同上 §P2 | 3-4 | 数据集卡片墙+证伪清单+泄漏链图 | — |
| P3 | 同上 §P3 | **3 起步（按主题簇）** | 思路总目录 N≈12-16 | 筛明显不可行 |
| P4 | 同上 §P4（3 个 persona） | **恒 3** | 评分汇总（均值/共识/分歧） | **选 TopN** |
| P5 | 同上 §P5 | **每案 1 个** | 逐案查重+三类拦截风险清单 | **继续/转向/降级** |
| P6 | 同上 §P6 | 每案 1 个 | 论文级方案（13 要素） | **立项裁决** |
| P7 | 同上 §P7 | 1-3 | 占坑窗口+监测清单 | 启动死线确认 |
| 终 | `templates/experiment-plan-template.md` | 1 | 训练端交接执行版 | — |

## 文件导航

- `references/pipeline-prompts.md` — P0-P7 全部阶段提示词（{{占位符}} 替换即用）
- `references/orchestration.md` — 蜂群编排：各阶段扇出表、共享上下文块、聚合器提示词、最小编排方案
- `references/pitfalls.md` — 编排纪律与常见坑（三轮实践教训，**开工前必读**）
- `templates/` — 四大产出物的通用骨架（方案/实验计划/评分/查新）+ 执行端开工指令
- `examples/case-structure.md` — 一个真实课题的三件套文档结构范例（脱敏）

## 快速开始（照抄即可跑一轮）

照 `references/orchestration.md` §8.5 的最小编排方案执行：
第 1 批并行 4（数据集×3 + 文献×1）→ 聚合 → 第 2 批并行 3（思路按主题簇）→ 聚合+人工筛 →
第 3 批并行 3（三专家评分）→ 聚合+人工选 Top5 → 第 4 批并行 5（逐案查重）→ 聚合+人工裁决 →
第 5 批方案展开 → 第 6 批窗口侦察 → 用实验计划模板产出交接版。

## 三条铁律（违反任何一条，整轮产出不可信）

1. **数据事实核查先于机制设计**：卖点必须绑定已核实存在的数据字段；二手口径必错；
   引用幻觉零容忍；幻影数据集要显式证伪。
2. **并行智能体提示词必须自包含**：互相看不见，"见上一阶段文档"要换成把内容粘进提示词；
   输出 schema 在扇出前统一；写隔离（子智能体只写自己的编号文件）。
3. **人在聚合点裁决**：TopN 选择、查重后继续/转向/降级、立项、启动死线——
   智能体负责把事实和选项做穷尽，这四个决定永远由人做。
