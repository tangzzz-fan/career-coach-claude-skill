---
description: Record a new funnel event (application sent, reply received, interview scheduled, etc.)
argument-hint: 渠道 公司 岗位 状态 [备注]. Example: "Boss直聘 某公司 目标岗位 已投递 主赛道版简历"
---

Invoke the career-coach skill in **funnel recording mode (模式四·漏斗记录)**.

**Workspace rule**: treat the current folder as the user's job-search workspace.
Write execution data only to `.career-coach/tracking/漏斗记录表.md`.

**Your task**:
1. Parse the funnel event from $ARGUMENTS: 渠道 公司 岗位 状态 [备注]
2. Append a new row to the detail table in `.career-coach/tracking/漏斗记录表.md`
3. Update the weekly summary row
4. Echo back: recorded + current week counts vs thresholds

**Hard constraints**:
- Do NOT automatically scan the workspace for resume/JD/story/interview-feedback files in this mode
- Do NOT perform content diagnosis here — this mode is execution-only

Fast in, fast out. Target: 10 seconds.

$ARGUMENTS
