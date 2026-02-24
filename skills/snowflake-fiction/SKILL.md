---
name: snowflake-fiction
description: 使用雪花写作法(Snowflake Method)创作小说。当用户说"写小说"、"创作故事"、"雪花法"、"帮我构思一个故事"时自动激活。支持短篇小说（1-3万字）、长篇小说（10万字+）和百万级网文（100万字+）的全流程创作。
version: 1.2.0
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

## 选择创作模式

```
/snowflake-fiction 短篇 帮我写一个都市职场故事
/snowflake-fiction 长篇 帮我写一个玄幻修仙小说，目标10万字
/snowflake-fiction 百万级 玄幻 300万字
/snowflake-fiction 百万级 番茄 都市 200万字 日更
```

### 番茄小说专项支持

当选择「百万级」模式并指定「番茄」平台时，额外提供：

| 支持项 | 说明 | 输出时机 |
|--------|------|----------|
| **推荐评估节点规划** | 8万字、15万字关键节点设计 | 步骤6-9 |
| **数据指标嵌入** | 追读率/完读率关注点设计 | 步骤10 |
| **书名简介优化** | 生成5套书名+简介组合（书测备用） | 步骤1-2 |
| **验证期存稿规划** | 确保验证期不断更 | 步骤10 |
| **黄金三章增强** | 按3秒法则设计开篇 | 步骤8-9 |

---

## 工作流程概览

### 短篇小说（12步）

| 阶段 | 步骤 | 输出物 | 委托子技能 |
|------|------|--------|-----------|
| **构思期** | 1-2 | 一句话概括 + 五句式大纲 | `outline-concept` |
| **设计期** | 3,5 | 人物卡片 + 背景故事 | `character-design` |
| **构建期** | 4,6,7 | 一页大纲 + 四页大纲 + 人物宝典 | `outline-builder` / `character-design` |
| **规划期** | 8-9 | 场景清单 + 场景规划 | `scene-plan` |
| **创作期** | 10 | 正式正文 | 内联（本文件） |
| **润色期** | 11 | 人语化处理 | `humanize-text` |
| **导出期** | 12 | 平台格式 | `novel-export` |

### 长篇小说（15步）

| 阶段 | 步骤 | 输出物 | 委托子技能 |
|------|------|--------|-----------|
| **构思期** | 1-2 | 一句话概括 + 五句式大纲 | `outline-concept` |
| **规模期** | 3 | 卷数规划 + 章节数量 | 内联 |
| **人物期** | 4-5 | 主角群卡片 + 配角群卡片 | `character-design` |
| **总纲期** | 6-7 | 一页总纲 + 各卷大纲 | `outline-builder` |
| **深化期** | 8-9 | 主角背景 + 配角背景 | `character-design` |
| **构建期** | 10-11 | 完整总大纲 + 人物宝典 | `outline-builder` / `character-design` |
| **规划期** | 12-14 | 卷级清单 + 章级大纲 + 场景规划 | `scene-plan` |
| **创作期** | 15 | 逐章生成 + 润色 | 内联 + `humanize-text` |

---

## 详细执行流程

### 第一阶段：构思期（步骤1-2）

#### 步骤 1-2：一句话概括 + 五句式大纲

**委托**：调用 `outline-concept` skill 执行此阶段。

**传入上下文**：用户提供的题材偏好、主角类型、核心冲突
**输出物**：`[小说名]/00-一句话概括.md`、`[小说名]/01-五句式大纲.md`
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

**目标**：按规划逐章生成正文

**执行原则**：
1. **逐章生成**：不一次性生成全文
2. **用户把控**：每章生成后确认再继续
3. **保持一致性**：检查人物设定、情节逻辑、伏笔收束

**单章生成流程**：
```
1. 读取该章的场景规划（08-场景规划/）
2. 读取相关人物宝典（06-人物宝典/）
3. 读取前文内容（保持连贯）
4. 生成初稿
5. 用户修改确认
6. 保存到 正文/第N章.md
```

**批量生成模式**（可选）：

```bash
/snowflake-fiction 生成 第5-10章 --batch
/snowflake-fiction 生成 第5-10章 --batch --concurrency 2
```

**并发控制策略**：

| 参数 | 说明 |
|------|------|
| `--batch` | 启用批量生成模式 |
| `--concurrency N` | 并发数量，默认 **2**（避免 API 限流） |

- 默认并发数：**2**，推荐范围：1-3，每章间隔：2 秒
- 遇到限流时：自动退避，等待 5 秒后重试，最多 3 次

---

### 第六阶段：润色期（步骤11）

#### 步骤 11：人语化处理

**委托**：调用 `humanize-text` skill 执行此步骤。

**传入上下文**：`正文/第N章.md`（逐章或批量）
**输出物**：覆盖原文件或输出到 `正文/第N章-润色.md`
**参考**：[humanize-text skill](../humanize-text/SKILL.md)

---

### 第七阶段：导出期（步骤12）

#### 步骤 12：导出投稿格式

**委托**：调用 `novel-export` skill 执行此步骤。

**传入上下文**：`正文/` 目录下所有章节文件
**输出物**：`export/[平台名]/` 目录下的格式化文件
**参考**：[novel-export skill](../novel-export/SKILL.md)

使用方式：
```
/snowflake-fiction 导出 番茄
/snowflake-fiction 导出 起点
/snowflake-fiction 导出 纯文本
/snowflake-fiction 导出 Word
```

---

## 输出目录规则

```
[当前工作目录]/
└── [小说名]/
    ├── 00-一句话概括.md        ← 步骤1（outline-concept）
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

## 并发控制策略

| 操作 | 默认并发 | 推荐范围 | 间隔时间 |
|------|----------|----------|----------|
| 批量生成章节 | 2 | 1-3 | 2 秒 |
| 批量导出格式 | 3 | 2-5 | 1 秒 |
| 人语化处理 | 2 | 1-3 | 1 秒 |

遇到 429 错误时自动退避，等待 5 秒后重试，最多 3 次。

---

## 相关资源

- [outline-concept skill](../outline-concept/SKILL.md)
- [character-design skill](../character-design/SKILL.md)
- [outline-builder agent](../../agents/outline-builder.md)
- [scene-plan skill](../scene-plan/SKILL.md)
- [humanize-text skill](../humanize-text/SKILL.md)
- [novel-export skill](../novel-export/SKILL.md)
- [每步提示词模板](./references/step-prompts.md)
- [长篇小说创作指南](./references/long-novel-guide.md)
- [百万级网文创作指南](./references/million-word-webnovel-guide.md)
- [番茄小说平台创作指南](./references/fanqie-guide.md)
