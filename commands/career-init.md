---
description: Initialize your Career Coach environment. Creates ~/career-plan/ directory structure, tracking templates, and starter plan documents. Run once after installation.
argument-hint: (optional) your macOS username, e.g. "andy" — only needed if different from whoami
---

You are setting up the Career Coach environment for the user. This is a one-time initialization — it is NOT a coaching session. Do NOT invoke the career-coach skill persona. Work directly with Bash, Write, and Read tools.

**Your task, in order**:

## Phase 1: Resolve username

Run `whoami` to get the current macOS username.
If $ARGUMENTS is non-empty, use $ARGUMENTS as the username instead.
Store this as `$USER`. All paths below use `/Users/$USER/` as the home prefix.

Print: "🔍 使用用户名: $USER"

## Phase 2: Survey what already exists

Check each of these paths and report status (exists / missing):

- `~/career-plan/tracking/每日状态.md`
- `~/career-plan/tracking/漏斗记录表.md`
- `~/career-plan/tracking/周复盘记录.md`
- `~/career-plan/求职执行计划.md`
- `~/career-plan/求职策略与定位.md`

Use `Bash(test -f <path> && echo "EXISTS" || echo "MISSING")` for each.

## Phase 3: Create directories

```
mkdir -p ~/career-plan/tracking
mkdir -p ~/career-plan/profile
```

## Phase 4: Write tracking templates (only if missing)

For each of the 3 tracking templates below: if the file does NOT already exist, write it. If it exists, skip it with "⏭️ already exists".

### tracking/每日状态.md
Write to `~/career-plan/tracking/每日状态.md` with the following content (replace {{TODAY}} with today's date from `date +%Y-%m-%d`, leave other {{PLACEHOLDERS}} as-is):

```
# 每日状态

> 最后更新：{{TODAY}}
> 此文件由职业教练 Skill 和 /career-checkin /career-checkout 命令自动维护

## 当前状态

- **当前周次**：第 1 周（{{START_DATE}} – {{END_DATE}}）
- **当前阶段**：简历去水 + 漏斗重启
- **连续执行天数**：0
- **今日日期**：{{TODAY}}
- **最后签到日期**：—
- **最后签退日期**：—
- **上次复盘日期**：—

## 今日三件事

1. 
2. 
3. 

## 昨日调整

（从昨日复盘继承：明天要调整的一件事）
*尚未开始*

## 今日漏斗

- 投递：
- 回复：
- 约面：

## 今日时间块执行

| 时段 | 计划动作 | 完成 |
|------|----------|------|
| 09:00-09:30 | 启动：更新漏斗表 + 写下3件事 | |
| 09:30-11:30 | 投递黄金档：≥20定向沟通 | |
| 11:30-12:30 | 跟进清零：猎头/内推/未读消息 | |
| 14:00-16:00 | 面试弹药：一条经历→五层故事 | |
| 16:00-17:30 | 周主题训练 | |
| 19:30-21:30 | 项目/技能学习推进 | |
| 21:30-21:45 | 复盘：记录漏斗 + 明日调整 | |

## 闸门状态

| 闸门 | 状态 | 触发条件 | 备注 |
|------|------|----------|------|
| 扩地域 + 降薪 | 🔒 未触发 | 第6周起评估 | |
| 现金闸门 | ⏳ 待评估 | 现金≤3月生活费 | 需手动告知当前现金状态 |
| 双轨实验 | 🔒 未开始 | 第4周末 | |
| 提前触发预警 | 🔒 未触发 | 连续2周约面<3 | |
| 中断三天警报 | 🔒 未触发 | 连续3+天未执行 | |

## 技能学习进度（可选）

- **当前阶段**：根据个人计划设定
- **本周学习目标**：根据个人计划设定
- **状态**：未开始
```

### tracking/漏斗记录表.md
Write to `~/career-plan/tracking/漏斗记录表.md`. If the file does not exist, first try to read the template from the project: Read the file at `templates/漏斗记录表.md` in the current project directory (try paths: `./templates/漏斗记录表.md`, then look in `.claude/../templates/漏斗记录表.md`). If you find it, copy its content directly (replacing {{TODAY}} with today's date). If you cannot find the template file, write a minimal funnel table with these sections:

- A detail table with columns: 序号 | 日期 | 渠道 | 公司 | 岗位 | 简历版本 | 状态 | 备注
- A weekly summary table with rows W1-W8, columns: 周次 | 日期范围 | 投递数 | 回复数 | 约面数 | 一面 | 二面 | 终面 | Offer | 回复率 | 约面率
- An interview record table with columns: 日期 | 公司 | 轮次 | 关键问题 | 答得好的 | 被问倒的 | 复盘笔记
- A referral/headhunter tracking table

### tracking/周复盘记录.md
Write to `~/career-plan/tracking/周复盘记录.md`. Similarly, try to read `templates/周复盘记录.md` from the project first. If unavailable, write a minimal weekly review template with indicator comparison tables for W1-W4 and a compact table for W5-W8.

## Phase 5: Write core plan documents (only if missing)

### 求职执行计划.md
If `~/career-plan/求职执行计划.md` does NOT exist, try to read `templates/求职执行计划.md` from the project directory. Replace `{{TODAY}}` with today's date, write to `~/career-plan/求职执行计划.md`. If the template file is not found, write a minimal version with these sections:

1. 三条铁律 (pre-filled from the coach framework)
2. 周指标底线 (with 🔧 placeholders for 5 metrics)
3. 阶段清单 (W1-W8 phase table)
4. 闸门触发条件 (G1-G5 descriptions)
5. 每日时间块 (reference template)
6. 五层故事清单 (8 slots with 🔧 placeholders)
7. 当前现金状态 (3 🔧 fields)
8. 简历版本 (3 🔧 fields)

### 求职策略与定位.md
If `~/career-plan/求职策略与定位.md` does NOT exist, try to read `templates/求职策略与定位.md` from the project directory. Replace `{{TODAY}}` with today's date, write to `~/career-plan/求职策略与定位.md`. If the template file is not found, write a minimal version with these sections:

1. 目标岗位定位 (3 🔧 fields)
2. 赛道选择 (table with 3 tracks)
3. 搜索关键词 (3 🔧 fields)
4. 目标城市 (3 🔧 fields)
5. 薪资策略 (4 🔧 fields including G2/G3 gate levels)
6. 目标公司清单 (empty table)
7. 简历版本策略 (profile/ path references)

## Phase 6: Settings file guidance

Check if `.claude/settings.example.json` exists in the project directory (try `./.claude/settings.example.json`, then relative paths from skill location). If found:

1. Read it
2. Get the user's actual username (from Phase 1 `$USER` or rerun `whoami`)
3. Replace `YOUR_USERNAME` with the actual username throughout the JSON
4. Print:

```
📋 你的个性化权限配置（把 YOUR_USERNAME 替换为了 $USER）：

```json
{the complete JSON with actual username substituted}
```

请将这段 JSON 添加到你的 settings 配置中：
- 项目级别：复制到项目目录的 .claude/settings.json
- 全局级别：合并到 ~/.claude/settings.local.json

权限说明：
- Read career-plan/** — 读取所有计划文档和追踪文件
- Write career-plan/tracking/** — 教练写入每日状态、漏斗、周复盘
- Write career-plan/*.md — 初始化时写入根级别计划文档
- Bash(mkdir ...) — 创建 career-plan 子目录
```

If `.claude/settings.example.json` is not found, tell the user to manually configure permissions per the README and list the required permission entries.

## Phase 7: Validation checklist

Print a final checklist:

```
═══════════════════════════════════
  Career Coach 环境初始化完成
═══════════════════════════════════

目录结构：
  {✅/⏭️} ~/career-plan/tracking/
  {✅/⏭️} ~/career-plan/profile/

追踪模板：
  {✅/⏭️} tracking/每日状态.md
  {✅/⏭️} tracking/漏斗记录表.md
  {✅/⏭️} tracking/周复盘记录.md

核心计划文档：
  {✅/⏭️} 求职执行计划.md
  {✅/⏭️} 求职策略与定位.md

═══════════════════════════════════

📝 下一步（5–10 分钟）：

1. 打开 ~/career-plan/求职执行计划.md
   找到所有 🔧 标记，填入你的数字和规则
   （最少必须填：第二节周指标底线）

2. 打开 ~/career-plan/求职策略与定位.md
   找到所有 🔧 标记，填入目标岗位和赛道

3. （可选）把简历放到 ~/career-plan/profile/简历-主赛道.md
   把目标 JD 放到 ~/career-plan/profile/JD-01-公司名.md
   仅在需要内容诊断时使用 /career-diagnose

4. 准备就绪后，运行 /career-checkin 开始第一天
```

For each file, use ✅ if you created it, ⏭️ if it already existed (preserved).

Close with: "开始执行。运行 `/career-checkin` 进入你的第一天。"

## Guardrails

- **NEVER overwrite existing files.** Always check with `test -f <path>` before writing.
- This is setup, not coaching. Do NOT invoke the career-coach skill persona.
- Do NOT read or write `profile/` files. The `profile/` directory is for user content.
- Replace `{{TODAY}}` with today's date. Leave all other {{PLACEHOLDERS}} untouched.
- Keep output concise — the user wants their environment ready, not a tutorial.

$ARGUMENTS
