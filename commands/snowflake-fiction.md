---
description: 使用雪花写作法(Snowflake Method)创作小说。当用户说"写小说"、"创作故事"、"雪花法"、"帮我构思一个故事"时自动激活。支持短篇小说（1-3万字）、长篇小说（10万字+）和百万级网文（100万字+）的全流程创作。
---

# 雪花写作法小说创作

本命令采用兰迪·英格曼森(Randy Ingermanson)提出的**雪花写作法**，通过循序渐进的步骤，从简单概念扩展为完整小说。

## 路由规则

根据用户输入类型，路由到不同处理层：

| 输入类型 | 示例 | 路由目标 | 说明 |
|---------|------|----------|------|
| 新建创作 | `/snowflake-fiction 短篇 都市职场` | **Skill** | 引导式创作流程 |
| 指定步骤 | `/snowflake-fiction 步骤3 反派角色` | **Skill** | 迭代式，重跑指定步骤 |
| 文件路径 | `/snowflake-fiction ./我的小说/` | **Agent** | 扫描目录，判断进度 |
| 批量生成 | `/snowflake-fiction 生成 第5-10章 --batch` | **Agent** | 并行子代理生成 |
| 导出 | `/snowflake-fiction 导出 番茄` | **Agent** | 路由到 novel-export |
| 无输入 | `/snowflake-fiction` | **Agent** | 扫描当前目录，交互引导 |

### 判断逻辑

```
输入包含路径（./、/、相对路径）→ 调用 agent（snowflake-fiction agent）
输入包含"生成"+"第X章"/"--batch" → 调用 agent
输入包含"导出" → 调用 agent（路由到 novel-export agent）
输入包含模式关键词（短篇/长篇/百万级）→ 调用 skill
输入包含"步骤X"/"重新生成" → 调用 skill
无输入 → 调用 agent（扫描当前目录）
```

---

## 三种创作模式

| 模式 | 字数范围 | 步骤数 | 适用场景 |
|------|----------|--------|----------|
| **短篇小说** | 1-3万字 | 12步 | 知乎盐选、短篇投稿 |
| **长篇小说** | 10-50万字 | 15步 | 传统出版、中篇网文 |
| **百万级网文** | 100万字+ | 15步+商业节奏 | 番茄、起点等平台 |

## 使用方式

```bash
# 新建创作（→ Skill）
/snowflake-fiction 短篇 帮我写一个都市职场故事
/snowflake-fiction 长篇 帮我写一个玄幻修仙小说，目标10万字
/snowflake-fiction 百万级 玄幻 300万字
/snowflake-fiction 百万级 番茄 都市 200万字 日更

# 指定步骤（→ Skill）
/snowflake-fiction 步骤3 反派角色
/snowflake-fiction 重新生成 步骤6

# 文件路径（→ Agent）
/snowflake-fiction ./我的小说/
/snowflake-fiction 输出到 ./my-novel/

# 批量生成（→ Agent）
/snowflake-fiction 生成 第5-10章 --batch
/snowflake-fiction 生成 第5-10章 --batch --concurrency 2

# 导出（→ Agent → novel-export）
/snowflake-fiction 导出 番茄
/snowflake-fiction 导出 起点

# 无输入（→ Agent，扫描当前目录）
/snowflake-fiction
```

## 番茄小说专项支持

当选择「百万级」模式并指定「番茄」平台时，额外提供：

| 支持项 | 说明 | 输出时机 |
|--------|------|----------|
| **推荐评估节点规划** | 8万字、15万字关键节点设计 | 步骤6-9 |
| **数据指标嵌入** | 追读率/完读率关注点设计 | 步骤10 |
| **书名简介优化** | 生成5套书名+简介组合（书测备用） | 步骤1-2 |
| **验证期存稿规划** | 确保验证期不断更 | 步骤10 |
| **黄金三章增强** | 按3秒法则设计开篇 | 步骤8-9 |

## 相关命令

| 命令 | 用途 |
|------|------|
| `/outline-concept` | 快速构思（步骤1-2） |
| `/character-design` | 角色设计（步骤3+5+7） |
| `/scene-plan` | 场景规划（步骤8+9） |
| `/novel-review` | 小说复核 |
| `/humanize-text` | 人语化处理 |
| `/quality-check` | 内容质量评估 |
| `/novel-export` | 导出平台格式 |

## 相关资源

- [snowflake-fiction skill](../skills/snowflake-fiction/SKILL.md)（核心编排知识库）
- [snowflake-fiction agent](../agents/snowflake-fiction.md)（文件处理器）
- [每步提示词模板](../skills/snowflake-fiction/references/step-prompts.md)
- [长篇小说创作指南](../skills/snowflake-fiction/references/long-novel-guide.md)
- [百万级网文创作指南](../skills/snowflake-fiction/references/million-word-webnovel-guide.md)
- [番茄小说平台创作指南](../skills/snowflake-fiction/references/fanqie-guide.md)

