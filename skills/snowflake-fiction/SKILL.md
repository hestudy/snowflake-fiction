---
name: snowflake-fiction
description: 使用雪花写作法(Snowflake Method)创作小说。当用户说"写小说"、"创作故事"、"雪花法"、"帮我构思一个故事"时自动激活。支持短篇小说（1-3万字）、长篇小说（10万字+）和百万级网文（100万字+）的全流程创作。
version: 1.3.0
---

# 雪花写作法小说创作 Skill（编排器）

本 Skill 是**纯编排器**，采用兰迪·英格曼森(Randy Ingermanson)的雪花写作法，将各阶段任务委托给对应子技能/agent 执行。

**支持三种模式**：
- **短篇小说**（1-3万字）：12步完成
- **长篇小说**（10-50万字）：15步完成，多卷结构
- **百万级网文**（100万字+）：商业节奏设计，持续更新策略

## 核心理念

```
一片雪花 ⟶ 从简单的三角形开始 ⟶ 不断细化扩展 ⟶ 形成精美图案
    ↓
一个创意 ⟶ 一句话概括 ⟶ 逐步深化 ⟶ 完整小说
```

---

## 工作流程概览

### 短篇小说（12步）

| 阶段 | 步骤 | 输出物 | 委托子技能 |
|------|------|--------|-----------|
| **构思期** | 1-2 | 一句话概括 + 五句式大纲 + 写作风格配置 | `outline-concept` |
| **设计期** | 3,5 | 人物卡片 + 背景故事 | `character-design` |
| **构建期** | 4,6,7 | 一页大纲 + 四页大纲 + 人物宝典 | `outline-builder` / `character-design` |
| **规划期** | 8-9 | 场景清单 + 场景规划 | `scene-plan` |
| **创作期** | 10 | 正式正文 | `chapter-write` |
| **润色期** | 11 | 人语化处理 | `humanize-text` |
| **导出期** | 12 | 平台格式 | `novel-export` |

### 长篇小说（15步）

| 阶段 | 步骤 | 输出物 | 委托子技能 |
|------|------|--------|-----------|
| **构思期** | 1-2 | 一句话概括 + 五句式大纲 + 写作风格配置 | `outline-concept` |
| **规模期** | 3 | 卷数规划 + 章节数量 | 内联 |
| **人物期** | 4-5 | 主角群卡片 + 配角群卡片 | `character-design` |
| **总纲期** | 6-7 | 一页总纲 + 各卷大纲 | `outline-builder` |
| **深化期** | 8-9 | 主角背景 + 配角背景 | `character-design` |
| **构建期** | 10-11 | 完整总大纲 + 人物宝典 | `outline-builder` / `character-design` |
| **规划期** | 12-14 | 卷级清单 + 章级大纲 + 场景规划 | `scene-plan` |
| **创作期** | 15 | 逐章生成 + 润色 | `chapter-write` + `humanize-text` |

---

## 详细执行流程

### 第一阶段：构思期（步骤1-2）

#### 步骤 1-2：一句话概括 + 五句式大纲

**委托**：调用 `outline-concept` skill 执行此阶段。

**传入上下文**：用户提供的题材偏好、主角类型、核心冲突
**输出物**：`[小说名]/00-一句话概括.md`、`[小说名]/00-写作风格.md`、`[小说名]/01-五句式大纲.md`
**参考**：[outline-concept skill](../outline-concept/SKILL.md)

---

### 第二阶段：设计期（步骤3,5）

#### 步骤 3：一页纸人物介绍 / 步骤 5：人物背景故事

**委托**：调用 `character-design` skill 执行步骤3和步骤5。

**传入上下文**：`01-五句式大纲.md`
**输出物**：`03-人物卡片/[角色名].md`、`04-人物背景/[角色名]-背景.md`
**参考**：[character-design skill](../character-design/SKILL.md)

---

### 第三阶段：构建期（步骤4,6,7）

#### 步骤 4：一页纸大纲 / 步骤 6：四页纸完整大纲

**委托**：调用 `outline-builder` agent 执行步骤4和步骤6。

**传入上下文**：`01-五句式大纲.md`、`03-人物卡片/`、`04-人物背景/`（agent 自主读取）
**输出物**：`02-一页纸大纲.md`、`05-完整大纲.md`
**参考**：[outline-builder agent](../../agents/outline-builder.md)

#### 步骤 7：人物宝典

**委托**：调用 `character-design` skill 执行步骤7。

**传入上下文**：`03-人物卡片/`、`04-人物背景/`
**输出物**：`06-人物宝典/[角色名]-宝典.md`
**参考**：[character-design skill](../character-design/SKILL.md)

---

### 第四阶段：规划期（步骤8-9）

#### 步骤 8：场景清单 / 步骤 9：场景规划

**委托**：调用 `scene-plan` skill 执行步骤8和步骤9。

**传入上下文**：`05-完整大纲.md`、`06-人物宝典/`
**输出物**：`07-场景清单.md`、`08-场景规划/场景[N]-[名].md`
**参考**：[scene-plan skill](../scene-plan/SKILL.md)

---

### 第五阶段：创作期（步骤10）

#### 步骤 10：正式写作

**委托**：调用 `chapter-write` agent 执行此阶段。

**传入上下文**：`08-场景规划/`、`06-人物宝典/`、`00-写作风格.md`、`正文/`（agent 自主读取）
**输出物**：`正文/第N章.md`
**参考**：[chapter-write skill](../chapter-write/SKILL.md) | [chapter-write agent](../../agents/chapter-write.md)

单章生成、批量生成和并发控制均由 chapter-write agent 负责。

---

### 第六阶段：润色期（步骤11）

#### 步骤 11：人语化处理

**委托**：
- 纯文本模式：调用 `humanize-text` skill 执行此步骤
- 文件模式：调用 `humanize-text` agent 并行处理章节文件

**传入上下文**：`正文/第N章.md`（逐章或批量）
**输出物**：覆盖原文件或输出到 `正文/第N章-润色.md`
**参考**：[humanize-text skill](../humanize-text/SKILL.md) | [humanize-text agent](../../agents/humanize-text.md)

---

### 第七阶段：导出期（步骤12）

#### 步骤 12：导出投稿格式

**委托**：调用 `novel-export` skill 执行此步骤。

**传入上下文**：`正文/` 目录下所有章节文件
**输出物**：`export/[平台名]/` 目录下的格式化文件
**参考**：[novel-export skill](../novel-export/SKILL.md)

---

## 输出目录规则

```
[当前工作目录]/
└── [小说名]/
    ├── 00-一句话概括.md        ← 步骤1（outline-concept）
    ├── 00-写作风格.md          ← 步骤1.5c（outline-concept）
    ├── 01-五句式大纲.md        ← 步骤2（outline-concept）
    ├── 02-一页纸大纲.md        ← 步骤4（outline-builder）
    ├── 03-人物卡片/            ← 步骤3（character-design）
    ├── 04-人物背景/            ← 步骤5（character-design）
    ├── 05-完整大纲.md          ← 步骤6（outline-builder）
    ├── 06-人物宝典/            ← 步骤7（character-design）
    ├── 07-场景清单.md          ← 步骤8（scene-plan）
    ├── 08-场景规划/            ← 步骤9（scene-plan）
    └── 正文/
        ├── 第1章.md
        └── 第2章.md
```

**目录处理规则**：
- 第一步执行时，直接在当前工作目录下以小说名创建子目录
- **向后兼容**：如已存在 `novel-output/[小说名]/`，自动识别并继续使用
- 用户可自定义：`/snowflake-fiction 输出到 ./my-novel/`

---

## 交互模式

### 模式 A：引导式（推荐新手）

逐步引导，每步完成后询问用户是否满意再继续。

### 模式 B：快速式（有经验的作者）

```
/snowflake-fiction 百万级 玄幻 直接到第6步
```

跳过前置步骤，直接从指定步骤开始。

### 模式 C：迭代式（灵活调整）

```
/snowflake-fiction 重新生成 步骤3 反派角色
```

单独重跑某一步骤，不影响其他已有内容。

---

## 相关资源

- [snowflake-fiction agent](../../agents/snowflake-fiction.md)（文件处理器：目录扫描、批量生成）
- [outline-concept skill](../outline-concept/SKILL.md)
- [character-design skill](../character-design/SKILL.md)
- [outline-builder agent](../../agents/outline-builder.md)
- [scene-plan skill](../scene-plan/SKILL.md)
- [chapter-write skill](../chapter-write/SKILL.md)
- [chapter-write agent](../../agents/chapter-write.md)
- [humanize-text skill](../humanize-text/SKILL.md)
- [humanize-text agent](../../agents/humanize-text.md)
- [novel-export skill](../novel-export/SKILL.md)
- [每步提示词模板](./references/step-prompts.md)
- [长篇小说创作指南](./references/long-novel-guide.md)
- [百万级网文创作指南](./references/million-word-webnovel-guide.md)
- [番茄小说平台创作指南](./references/fanqie-guide.md)
