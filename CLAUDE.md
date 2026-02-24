# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

Snowflake Fiction 是一个 Claude Code 插件，提供完整的小说创作工具链。包含四个核心技能：

| 技能 | 用途 | 触发词 |
|------|------|--------|
| snowflake-fiction | 雪花写作法创作小说 | 写小说、创作故事、雪花法 |
| novel-review | 小说质量复核检查 | 小说复核、章节检查、一致性检查、质量检查 |
| humanize-text | AI文本人语化处理 | 人语化、去AI味、润色 |
| novel-export | 导出各平台格式 | 导出小说、番茄格式、起点格式 |

## 目录结构

```
snowflake-fiction/
├── .claude-plugin/
│   ├── plugin.json           # 插件元数据
│   └── marketplace.json      # Marketplace 发布配置
├── skills/
│   ├── snowflake-fiction/    # 雪花写作法主技能
│   │   ├── SKILL.md          # 技能定义（12步/15步流程）
│   │   └── references/       # 参考模板
│   │       ├── step-prompts.md              # 每步提示词
│   │       ├── character-template.md        # 人物卡片模板
│   │       ├── scene-template.md            # 场景规划模板
│   │       ├── export-format.md             # 导出格式说明
│   │       ├── long-novel-guide.md          # 长篇小说指南
│   │       └── million-word-webnovel-guide.md # 百万级网文指南
│   ├── novel-review/         # 小说复核技能
│   │   ├── SKILL.md          # 技能定义（子代理架构）
│   │   └── references/
│   │       ├── consistency-check-prompt.md  # 一致性检查提示词
│   │       ├── character-state-template.md  # 角色状态追踪
│   │       ├── timeline-template.md         # 时间线追踪
│   │       ├── foreshadowing-tracker.md     # 伏笔追踪
│   │       └── review-report-template.md    # 复核报告模板
│   ├── humanize-text/        # 人语化处理技能
│   │   └── SKILL.md
│   └── novel-export/         # 格式导出技能
│       └── SKILL.md
└── README.md                 # 使用文档
```

## 技能架构

### snowflake-fiction（雪花写作法）

支持三种模式：
- **短篇小说**（1-3万字）：12步流程
- **长篇小说**（10-50万字）：15步流程，多卷结构
- **百万级网文**（100万字+）：商业节奏设计，黄金三章、付费卡点、爽点密度

流程阶段：构思期 → 设计期 → 构建期 → 规划期 → 创作期 → 润色期 → 导出期

输出目录规则：直接在当前工作目录下创建 `[小说名]/`（不再创建 `novel-output/` 中间层）；向后兼容已有的 `novel-output/[小说名]/` 结构

### novel-review（小说复核）

**核心挑战**：长篇小说可能有数十万字，一次性加载所有内容会导致上下文溢出。

**解决方案**：使用子代理（Sub-agent）架构，将检查任务拆分为独立的小任务。

检查项目：
- 角色一致性：性格、对话、能力、关系
- 时间线：时间流逝、季节、年龄
- 设定一致性：能力体系、物品、地点、规则
- 大纲偏离：核心事件、支线、节奏
- 伏笔回收：埋设、回收、超期预警
- 文风一致性：视角、语言风格、AI痕迹

输出目录规则：在小说目录下创建 `review/` 子目录，包含追踪文件和报告

### humanize-text（人语化处理）

核心指标：
- 困惑度（Perplexity）：避免过于常见的词汇选择
- 爆发度（Burstiness）：句式长短交替，节奏变化

支持场景：小说对话、小红书、学术论文、商务邮件

### novel-export（格式导出）

支持平台：番茄小说、起点中文网、晋江文学城、知乎盐选、七猫小说、通用纯文本、Word

关键格式差异：
- 番茄：无缩进，回车分段，无空行
- 起点：首行缩进2字符（全角空格）

## 修改技能时的注意事项

1. **SKILL.md 格式**：文件开头需包含 YAML front matter（name、description、version）
2. **触发词同步**：修改 description 中的触发词时，确保 README.md 也同步更新
3. **references 引用**：SKILL.md 中引用的模板文件路径使用相对路径 `./references/xxx.md`
4. **人语化禁止词汇**：保持 humanize-text 中禁止词汇清单的一致性

## 推荐工作流

```
snowflake-fiction → novel-review → humanize-text → novel-export
      ↑                  ↓
      └── 根据反馈修改 ←─┘
```

完整创作流程：
- 规划阶段（一次性）：使用 snowflake-fiction 完成大纲规划
- 日常生产（循环）：生成初稿 → 复核检查 → 人语化 → 导出 → 发布
- 周期回顾（每10章）：全面质量检查，调整大纲
