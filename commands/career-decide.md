---
description: Get structured decision support from your career coach on a job search decision.
argument-hint: Your decision question, e.g. "要不要接受这个offer" "该不该转向另一个方向"
---

Invoke the career-coach skill in **decision support mode (模式五·决策支持)**.

**Workspace rule**: treat the current folder as the user's job-search workspace.
Default inputs are the local rule and tracking files under `.career-coach/`.

**Your task**:
1. Read relevant sections from `.career-coach/求职执行计划.md` and `.career-coach/求职策略与定位.md`
2. Read current funnel data from `.career-coach/tracking/漏斗记录表.md`
3. Frame the analysis:
   - **预先承诺的规则怎么说？** — check iron laws and gate triggers first
   - **当前数据怎么说？** — what do the numbers show
   - **选项 A / B / C** — expected outcome, probability, downside, reversibility
   - **建议** — clearly labeled as advice, not overriding any pre-committed rules
4. If the user's pre-committed rules already answer this (e.g. cash gate triggered → accept any qualifying offer), point this out explicitly

Important: Do NOT override any pre-committed gate triggers or iron laws. Do NOT automatically scan the workspace for resume/JD files in this mode.

$ARGUMENTS
