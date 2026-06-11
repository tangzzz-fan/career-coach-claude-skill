---
description: Close out your job search. Generate a career asset package — summary report, reusable narratives, decision rules, and next-phase roadmap. Run once when you accept an offer or end your search.
argument-hint: (optional) final result, e.g. "接受了字节iOS 35K"
---

Invoke the career-coach skill in **career closeout mode (模式七·求职收官)**.

**Your task**:

## Phase 1: Confirm closeout status

Ask the user (if not provided in $ARGUMENTS):
- Accepted an offer? Which company, role, compensation (voluntary)?
- Or pausing/ending the search for another reason?
- Confirm they want to proceed — this is a one-time endpoint, not a daily mode.

## Phase 2: Collect source data (read-only)

Read ALL of the following to build a complete picture:

From `tracking/`:
- `tracking/漏斗记录表.md` — full cycle funnel data
- `tracking/每日状态.md` — execution continuity, gate states
- `tracking/周复盘记录.md` — weekly trends and adjustments

From `~/career-plan/` root:
- `求职执行计划.md` — original thresholds, iron laws, gate rules
- `求职策略与定位.md` — track selection, keywords, salary strategy

From `profile/`:
- All `profile/简历-*.md` files — resume versions used
- All `profile/JD-*.md` files — target JDs applied to
- `profile/项目故事库.md` — project story inventory
- All `profile/面试反馈-*.md` files — interview feedback collected

## Phase 3: Generate 4 closeout assets

Write ALL of the following to `~/career-plan/archive/`. If `archive/` doesn't exist, create it with `mkdir -p`. If any file already exists, append `-{YYYY-MM-DD}` to the filename.

### Asset 1: `archive/求职总结报告.md`

Generate with these sections:
```
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

{from weekly review records — which action or adjustment most changed the funnel trajectory}

## 本轮最大教训

{If you could do it again, what's the ONE thing you would change first}
```

### Asset 2: `archive/职业资产包.md`

Generate with these sections:
```
# 职业资产包

> 可复用于：下次求职、晋升述职、内部转岗、个人品牌

## 简历版本清单

| 版本 | 文件 | 定位 | 适用赛道 | 本轮效果 |
|------|------|------|----------|----------|
{extracted from profile/简历-*.md and funnel data}

## 项目故事库

| 故事 | 来源项目 | 使用频率 | 状态 |
|------|----------|----------|------|
| {story 1} | {project} | 高频/中频/低频 | ✅ 可用 / ⚠️ 需改进 / ❌ 未被问过 |
...

## 自我介绍模板

### 1 分钟版
{synthesized from profile/ data and interview feedback}

### 3 分钟版
{synthesized}

## 高频面试题

| 类别 | 题目 | 出现次数 | 表现 |
|------|------|----------|------|
| 技术 | {q} | {n} | ✅ / ⚠️ / ❌ |
| 项目 | {q} | {n} | ✅ / ⚠️ / ❌ |
| 行为 | {q} | {n} | ✅ / ⚠️ / ❌ |
| 算法 | {q} | {n} | ✅ / ⚠️ / ❌ |

## 薪资谈判记录

| 公司 | 初始报价 | 最终结果 | 谈判关键点 |
|------|----------|----------|------------|
{only if user provides this data}
```

### Asset 3: `archive/决策规则清单.md`

Generate with these sections:
```
# 决策规则清单

> 这些规则在本轮求职中得到验证。下次可直接复用，不需重新和焦虑谈判。

## 已验证有效的闸门

{list each gate from 求职执行计划.md with: original condition, whether it triggered, result of triggering, whether to keep/adjust/discard}

## 个人底线

| 维度 | 底线值 |
|------|--------|
| 现金安全线 | ≤ {N} 个月生活费时必须止血 |
| 最低可接受薪资 | {X} |
| 地域红线 | {cities} |
| 赛道禁区 | {tracks to avoid} |

## Offer 接受标准

- 必须满足：{conditions}
- 加分项：{conditions}
- 一票否决：{conditions}

## 下次应新增的规则

{from gaps identified in this cycle}
```

### Asset 4: `archive/下一阶段发展建议.md`

Generate with these sections:
```
# 下一阶段发展建议

## 入职前 30 天

{3-5 action items: skills to brush up, people to connect with, docs to prepare}

## 转正前 90 天

{key milestones, risk flags, and check-in points}

## 下次跳槽前应提前准备的 3 件事

1. {item}
2. {item}
3. {item}

## 本轮暴露的内容弱项

{extracted from 面试反馈-*.md — patterns of questions consistently answered poorly}
→ 建议纳入长期学习计划
```

## Phase 4: Archive raw tracking data

Copy the three tracking files to `archive/raw/`:
- `tracking/每日状态.md` → `archive/raw/每日状态.md`
- `tracking/漏斗记录表.md` → `archive/raw/漏斗记录表.md`
- `tracking/周复盘记录.md` → `archive/raw/周复盘记录.md`

Replace any remaining {{PLACEHOLDER}} values with actual data or "N/A".

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
- All asset writes go to `archive/` — never modify `tracking/` files
- Do NOT read from `archive/` during daily modes — archive is end-of-cycle only

$ARGUMENTS
