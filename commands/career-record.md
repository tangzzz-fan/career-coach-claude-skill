---
description: Record a new funnel event (application sent, reply received, interview scheduled, etc.)
argument-hint: 渠道 公司 岗位 状态 [备注]. Example: "Boss直聘 某公司 目标岗位 已投递 主赛道版简历"
---

Invoke the career-coach skill in **funnel recording mode (模式四·漏斗记录)**.

**Your task**:
1. Parse the funnel event from $ARGUMENTS: 渠道 公司 岗位 状态 [备注]
2. Append a new row to the detail table in `tracking/漏斗记录表.md`
3. Update the weekly summary row
4. Echo back: recorded + current week counts vs thresholds

Fast in, fast out. Target: 10 seconds.

$ARGUMENTS
