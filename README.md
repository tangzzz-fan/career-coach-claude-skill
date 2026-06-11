# Career Coach — Claude Code Skill

> 一个基于 Claude Code 的职业发展教练系统。帮你执行求职计划，而不是重新谈判。

## 这是什么？

**Career Coach** 是一个 Claude Code 自定义 skill，它会读取你的求职计划文档和追踪数据，像一个严格的教练一样推动你执行。分为两层：

- **执行引擎**（日常）：每日签到、晚间复盘、漏斗记录、周六周复盘、决策支持
- **诊断引擎**（按需）：简历匹配、故事质量、JD 定位——仅在 `/career-diagnose` 中触发

核心理念：
- **调整只看每周六的漏斗数据，不看当天情绪**
- **预先承诺的规则只能执行，不能谈判**
- **降低执行摩擦比增强意志力更有效**

## 功能概览

| 命令 | 功能 | 耗时 |
|------|------|------|
| `/career-checkin` | 晨间启动：确认今日三件事 + 漏斗进度 | 30 秒 |
| `/career-checkout` | 晚间复盘：记录漏斗数字 + 明天调整一项 | 2 分钟 |
| `/career-record` | 快速记录一次投递/回复/约面事件 | 10 秒 |
| `/career-review` | 周六周复盘：五项指标对照 + 趋势 + 闸门评估 | 15 分钟 |
| `/career-decide` | 结构化决策支持：不替你决定，帮你分析 | 按需 |
| `/career-diagnose` | 内容诊断：简历匹配、故事质量、JD 定位 | 5–8 分钟 |

### 架构：两个引擎

Career Coach 将能力分为两层：

- **执行引擎**（模式一～五，默认）：盯执行状态与数字偏差，不判断内容质量
- **诊断引擎**（模式六，按需）：分析简历/JD/故事/面试反馈，不修改闸门规则

执行引擎发现漏斗异常时，会提示是否需要触发诊断——但不会自动诊断。两个引擎的上下文空间不共享。

- **5 道闸门**：现金预警、地域/薪资扩展、双轨再平衡、提前触发、中断警报等
- **6 种反模式**：情绪化改策略、简历注水、拒绝算法面、用规划替代行动、自责螺旋、同时做太多
- **执行/诊断隔离**：日常模式只读追踪数据，绝不自动加载简历；内容诊断只能在独立模式中触发

## 安装

### 1. 复制 skill 文件

```bash
mkdir -p ~/.claude/skills/career-coach
cp skills/career-coach/SKILL.md ~/.claude/skills/career-coach/
```

### 2. 复制命令文件

```bash
mkdir -p ~/.claude/commands
cp commands/career-*.md ~/.claude/commands/
```

### 3. 创建计划目录和追踪文件

```bash
mkdir -p ~/career-plan/tracking
mkdir -p ~/career-plan/profile
cp templates/每日状态.md ~/career-plan/tracking/
cp templates/漏斗记录表.md ~/career-plan/tracking/
cp templates/周复盘记录.md ~/career-plan/tracking/
```

### 4. 配置权限

将 `.claude/settings.example.json` 中的内容添加到你的项目或用户 `settings.json` 中，把 `YOUR_USERNAME` 替换为你的实际用户名。

### 5. 创建你的计划文档

在 `~/career-plan/` 目录下创建以下文档（至少需要前两个）：

| 文档 | 用途 |
|------|------|
| `求职执行计划.md` | 每日节奏、周指标底线、阶段清单、铁律 |
| `求职策略与定位.md` | 定位标签、赛道选择、搜索关键词 |
| `策略分析文档.md` | （可选）JD分析参考 |

## 自定义

### 周指标底线

在 `求职执行计划.md` 中设定你的五个底线指标：
- 投递数 ≥ ? /周
- 回复数 ≥ ? /周
- 约面数 ≥ ? /周
- 二面数 ≥ ? /周（第3周起）
- 五层故事累计 ≥ ?（第2周末）

### 闸门触发条件

修改 `career-coach/SKILL.md` 中「闸门触发逻辑」部分的条件和动作，适配你的实际情况。

### 反模式

如果你有额外的行为模式需要教练检测，在「反模式检测」部分添加新的 AP。

## 文件结构

```
~/
├── .claude/
│   ├── skills/
│   │   └── career-coach/
│   │       └── SKILL.md          # 教练系统定义
│   └── commands/
│       ├── career-checkin.md     # 晨间签到
│       ├── career-checkout.md    # 晚间复盘
│       ├── career-record.md      # 漏斗记录
│       ├── career-review.md      # 周复盘
│       ├── career-decide.md      # 决策支持
│       └── career-diagnose.md    # 内容诊断
└── career-plan/                  # 你的计划文档（自己创建和维护）
    ├── 求职执行计划.md
    ├── 求职策略与定位.md
    ├── tracking/
    │   ├── 每日状态.md           # 教练自动维护
    │   ├── 漏斗记录表.md         # 教练自动维护
    │   └── 周复盘记录.md         # 教练自动维护
    └── profile/                  # （可选）按需诊断数据
        ├── 简历主档.md           # 仅 /career-diagnose 读取
        ├── 目标岗位JD.md
        ├── 项目故事库.md
        └── 面试反馈.md
```

## 使用示例

```bash
# 早上开始
/career-checkin 1.投递20个目标岗位 2.写核心项目五层故事 3.约前同事内推

# 投了一个岗位，快速记录
/career-record Boss直聘 某科技公司 iOS开发工程师 已投递 主赛道版简历

# 收到回复了
/career-record Boss直聘 某科技公司 iOS开发工程师 已回复

# 晚上收工
/career-checkout 投递22 回复3 约面0

# 周六复盘
/career-review

# 做决定
/career-decide 要不要接受目前唯一的offer还是继续面

# 内容诊断
/career-diagnose 为什么回复率这么低
```

## 原理

Career Coach 利用了 Claude Code 的 skill 系统：SKILL.md 定义了一个完整的 agent 人物设定、工作流、规则引擎。slash command 是进入特定模式的快捷方式。

教练**不存储你的数据**——它通过读写 `~/career-plan/tracking/` 下的 markdown 文件来追踪状态。你的数据完全在本地。

## 语言

当前版本为中文。欢迎贡献英文翻译。

## 协议

MIT — 自由使用、修改、分发。
