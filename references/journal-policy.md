# 期刊质量控制政策（Venue QC）

> 背景：实际使用中，智能体反复把 J Pathol Inform（细分对口但低档）、Computers in
> Biology and Medicine（已被 SCIE 除名）等期刊当作投稿目标。根因有二：
> ①**检索池锚定**——按主题检索命中的论文天然集中在小众 OA 刊；②**OA 超额代表**——
> 能抓到全文的多为开放获取刊，进一步扭曲池子；③期刊收录状态是动态的，
> 模型训练数据可能滞后（CBM 2025 年被 Clarivate 处置时，多数模型仍视其为正常期刊）。

## 规则一：目标期刊只来自 P0

检索池里出现的期刊 = 证据与语境，**不是投稿目标**。主题相关 ≠ 期刊合格。
P1 的"配方归纳"只提炼**方法组合**，不得从检索池继承投稿去向。
P4 评分中"期刊匹配度"一律对照 P0 声明的期刊档位清单打分。

## 规则二：任何期刊进入产出物前过四道检查（附查证日期与来源）

1. **收录状态**：在 Web of Science Core Collection 在库（Clarivate Master Journal List 实时查询）
2. **风险状态**：不在 Clarivate "on hold / delisted" 处置名单；不在《国际期刊预警名单》
   （中科院文献情报中心，每年初更新）
3. **档位匹配**：CAS 分区 / IF 带宽不低于委托人 P0 声明的下限
4. **出版商风险**：掠夺性出版商筛查（Beall 沿革名单 / DOAJ 除名记录）、
   喷涌式扩刊迹象（年发文量异常增长）

## 起步参考清单（**快照性质，使用时必须复核**——除名/预警每年都在变）

### 直接排除（截至 2026-10 快照）
- **Computers in Biology and Medicine (CBM)**：2025 年 Clarivate on-hold，随后已从 SCIE 除名
- Hindawi 系残留（2023-24 大规模除名后仍在消化）、Cureus、Heliyon（on-hold 风险）
- 曾上中科院预警名单且未洗白的期刊（每年名单发布后更新本清单）

### 谨慎/低档（默认不作为投稿目标，除非委托人明确要 informatics/细分定位）
- **J Pathol Inform**：主题高度对口但影响因子低档——这类"细分对口小刊"是
  检索池锚定偏差的重灾区
- MDPI 系（Diagnostics / Bioengineering / Cancers 等）：部分机构职称评审不认可
- 其他"主题高相关但档位低"的 OA 刊

### 档位锚示例（按 P0 声明替换）
- 临床顶档：Radiology / Lancet Digital Health / npj Digital Medicine
- 影像方法：Medical Image Analysis / IEEE TMI / Radiology:AI
- CS 优良：Knowledge-Based Systems / Pattern Recognition / EAAI / ESWA
- 数据档：Scientific Data

## 输出纪律

- P1 配方归纳：只提炼方法组合，**不产生投稿建议**
- P5 查新：最近邻表照常引用低档期刊论文（作为先行工作证据），但**期刊名旁标注档位**
- P6 投稿计划：所有候选期刊附 QC 四检查的通过记录（查证日期 + 查证来源 URL）；
  未过检查的期刊不得出现在推荐位
- 涉及"已被除名期刊上的近期论文"时，照常引用但加一句期刊状态说明
  （除名不影响已发表论文的学术效力，但影响"该刊是活跃发表地"的暗示）
