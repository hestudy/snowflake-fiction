---
description: 小说质量复核工具，检查角色一致性、时间线、设定冲突、大纲偏离、伏笔回收等问题。当用户说"小说复核"、"章节检查"、"一致性检查"、"质量检查"、"小说质检"时自动激活。使用子代理架构，支持长篇小说的增量检查。
---

# 小说复核

对已创作的小说内容进行质量检查，主要解决长篇小说创作中的**一致性维护**问题。

## 路由规则

根据用户输入类型，路由到不同处理器：

| 输入类型 | 示例 | 路由目标 |
|---------|------|----------|
| 文件路径 | `/novel-review ./我的小说/` | `agents/novel-review.md`（文件处理器） |
| 路径+章节 | `/novel-review ./我的小说/ 第3-5章` | `agents/novel-review.md`（文件处理器） |
| 路径+检查项 | `/novel-review ./我的小说/ --角色` | `agents/novel-review.md`（文件处理器） |
| 仅章节号 | `/novel-review 第10章` | `agents/novel-review.md`（当前目录查找） |
| 交互式 | `/novel-review` | `agents/novel-review.md`（交互式引导） |
| 纯文本 | `/novel-review [文本内容]` | `skills/novel-review/SKILL.md`（直接检查） |

### 判断逻辑

```
输入包含路径（./、/、相对路径）→ 调用 agent
输入包含"第X章"、"chapter"等关键词 → 调用 agent
输入包含检查项标志（--角色、--时间线等）→ 调用 agent
输入是纯文本 → 调用 skill（直接检查）
无输入 → 调用 agent（交互式引导）
```

## 检查项目

| 检查项 | 标志 | 说明 |
|--------|------|------|
| 角色一致性 | `--角色` | 性格、对话、能力、关系前后一致 |
| 时间线 | `--时间线` | 时间流逝、季节、年龄连贯 |
| 设定一致性 | `--设定` | 能力体系、物品、地点、规则 |
| 大纲偏离 | `--大纲` | 核心事件、支线、节奏是否符合规划 |
| 伏笔回收 | `--伏笔` | 埋设、回收、超期预警 |
| 文风一致性 | `--文风` | 视角、语言风格、AI痕迹、流水账检测 |
| 开篇质量 | `--开篇` | 黄金三章检查（仅前3章） |
| 评估准备 | `--评估准备` | 番茄平台推荐评估准备度检查 |
| 全面检查 | `--全文` | 所有检查项 |

## 使用方式

```bash
# 基础用法
/novel-review                              # 交互式引导
/novel-review ./我的小说/                   # 指定项目目录（全面检查）
/novel-review 第10章                        # 只检查指定章节
/novel-review 第5-10章                      # 检查章节范围

# 指定检查项
/novel-review --角色                        # 只检查角色一致性
/novel-review --时间线                      # 只检查时间线
/novel-review --全文                        # 全面检查

# 并发控制
/novel-review --parallel 1                 # 串行执行（最保守）
/novel-review --parallel 2                 # 每批2个（默认）

# 输出格式
/novel-review --report                     # 生成完整报告
/novel-review --quick                      # 快速检查（摘要模式）
/novel-review --json                       # 输出 JSON 格式
```

## 日常检查建议

| 场景 | 推荐命令 | 子代理数 |
|------|----------|----------|
| 每章检查 | `--角色` | 1 |
| 每5章检查 | `--角色 --时间线` | 2 |
| 每10章检查 | `--全文 --parallel 1` | 串行 |
| 8万字节点（番茄） | `--评估准备` | 1 |
| 完本前检查 | `--全文` | 分批 |

## 相关命令

| 需求 | 使用 |
|------|------|
| 人语化处理 | `/humanize-text [路径]` |
| 综合质量检查 | `/quality-check [文本]` |
| 流水账检测 | `/boring-detect [文本]` |
| 开篇检查 | `/opening-check [文本]` |

## 相关资源

- 核心知识库：`skills/novel-review/SKILL.md`
- 文件处理器（子代理架构）：`agents/novel-review.md`
- 检查提示词模板：`skills/novel-review/references/consistency-check-prompt.md`
- 报告模板：`skills/novel-review/references/review-report-template.md`
