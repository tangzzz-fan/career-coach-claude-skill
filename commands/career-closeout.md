---
description: Close out your job search. Generate a career asset package — summary report, reusable narratives, decision rules, and next-phase roadmap. Run once when you accept an offer or end your search.
argument-hint: (optional) final result, e.g. "接受了字节iOS 35K"
---

Invoke the career-coach skill in **career closeout mode (模式七·求职收官)**.

**Workspace rule**: treat the current folder as the user's job-search workspace.
Read source data from the visible workspace layer plus `.career-coach/`, then write all generated assets to `.career-coach/archive/`.

**Your task**:

## Phase 1: Confirm closeout status

Ask the user (if not provided in $ARGUMENTS):
- Accepted an offer? Which company, role, compensation (voluntary)?
- Or pausing/ending the search for another reason?
- Confirm they want to proceed — this is a one-time endpoint, not a daily mode.

## Phase 2: Collect source data (read-only)

Read ALL of the following to build a complete picture:

From `.career-coach/`:
- `.career-coach/tracking/漏斗记录表.md`
- `.career-coach/tracking/每日状态.md`
- `.career-coach/tracking/周复盘记录.md`
- `.career-coach/求职执行计划.md`
- `.career-coach/求职策略与定位.md`

From the workspace visible layer:
- All `简历-*.md` files (fallback: `profile/简历-*.md`)
- All `JD-*.md` files (fallback: `profile/JD-*.md`)
- `项目故事库.md` (fallback: `profile/项目故事库.md`)
- All `面试反馈-*.md` files (fallback: `profile/面试反馈-*.md`)

## Phase 3: Generate 4 closeout assets

Write ALL of the following to `.career-coach/archive/`. If `.career-coach/archive/` doesn't exist, create it. If any file already exists, append `-{YYYY-MM-DD}` to the filename.

- `.career-coach/archive/求职总结报告.md`
- `.career-coach/archive/职业资产包.md`
- `.career-coach/archive/决策规则清单.md`
- `.career-coach/archive/下一阶段发展建议.md`

Use the following concrete structures when generating the 4 assets:

### Asset 1: `求职总结报告.md`

```md
# 求职总结报告

> 周期：{start_date} – {end_date}（共 {N} 周）
> 生成日期：{today}

## 关键数字

| 指标 | 数值 |
|------|------|
| 总投递数 | {A} |
| 总回复数 | {B} |
| 总约面数 | {C} |
| 总面试轮次 | {D} |
| Offer 数 | {E} |

## 漏斗转化

| 阶段 | 转化率 |
|------|--------|
| 投递 → 回复 | {X}% |
| 回复 → 约面 | {Y}% |
| 约面 → 一面 | {Z1}% |
| 一面 → 二面 | {Z2}% |
| 二面 → 终面 | {Z3}% |
| 终面 → Offer | {Z4}% |

## 最终结果

- 接受 offer：{company} · {role} · {compensation（如提供）}
- 或：{结束原因}

## 本轮最大转折点

{哪个动作或调整改变了漏斗走向}

## 本轮最大教训

{如果再做一次，第一件会改什么}
```

### Asset 2: `职业资产包.md`

```md
# 职业资产包

> 可复用于：下次求职、晋升述职、内部转岗、个人品牌

## 简历版本清单

| 版本 | 文件 | 定位 | 适用赛道 | 本轮效果 |
|------|------|------|----------|----------|
| {version} | {file} | {positioning} | {track} | {effect} |

## 项目故事库

| 故事 | 来源项目 | 使用频率 | 状态 |
|------|----------|----------|------|
| {story} | {project} | 高频/中频/低频 | ✅ 可用 / ⚠️ 需改进 / ❌ 未被问过 |

## 自我介绍模板

### 1 分钟版
{synthesized intro}

### 3 分钟版
{synthesized intro}

## 高频面试题

| 类别 | 题目 | 出现次数 | 表现 |
|------|------|----------|------|
| 技术/项目/行为/算法 | {question} | {n} | ✅ / ⚠️ / ❌ |

## 薪资谈判记录

| 公司 | 初始报价 | 最终结果 | 谈判关键点 |
|------|----------|----------|------------|
| {company} | {offer} | {result} | {notes} |
```

Only include the salary negotiation table if the user provided the relevant data.

### Asset 3: `决策规则清单.md`

```md
# 决策规则清单

> 这些规则在本轮求职中得到验证。下次可直接复用，不需重新和焦虑谈判。

## 已验证有效的闸门

| 闸门 | 原始条件 | 是否触发 | 结果 | 下次建议 |
|------|----------|----------|------|----------|
| {gate} | {condition} | 是/否 | {result} | 保留/调整/移除 |

## 个人底线

| 维度 | 底线值 |
|------|--------|
| 现金安全线 | ≤ {N} 个月生活费时必须止血 |
| 最低可接受薪资 | {X} |
| 地域红线 | {cities} |
| 赛道禁区 | {tracks} |

## Offer 接受标准

- 必须满足：{conditions}
- 加分项：{conditions}
- 一票否决：{conditions}

## 下次应新增的规则

{from gaps identified in this cycle}
```

### Asset 4: `下一阶段发展建议.md`

```md
# 下一阶段发展建议

## 入职前 30 天

{3-5 action items}

## 转正前 90 天

{milestones, risks, check-in points}

## 下次跳槽前应提前准备的 3 件事

1. {item}
2. {item}
3. {item}

## 本轮暴露的内容弱项

{patterns extracted from interview feedback}
→ 建议纳入长期学习计划
```

## Phase 4: Archive raw tracking data

Copy the three tracking files to `.career-coach/archive/raw/`:
- `.career-coach/tracking/每日状态.md` → `.career-coach/archive/raw/每日状态.md`
- `.career-coach/tracking/漏斗记录表.md` → `.career-coach/archive/raw/漏斗记录表.md`
- `.career-coach/tracking/周复盘记录.md` → `.career-coach/archive/raw/周复盘记录.md`

Replace any remaining {{PLACEHOLDER}} values with actual data or `N/A`.

## Phase 5: Print summary

Use the output format specified in SKILL.md 模式七:
- Key numbers table
- Funnel conversion chain
- Final result
- List of 4 generated assets with ✅
- Closing message: "这些资产是你下次职业变动时可以直接复用的操作系统。"

## Hard constraints

- Do NOT modify gate rules — closeout is summarization, not renegotiation
- Do NOT overwrite existing archive files — append `-{date}` suffix if needed
- Compensation and sensitive data: only include if user explicitly provides it
- All asset writes go to `.career-coach/archive/` — never modify daily tracking files
- Do NOT read from `.career-coach/archive/` during daily modes — archive is end-of-cycle only

$ARGUMENTS
