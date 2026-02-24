---
description: 将AI生成的文本进行人语化处理，去除机器味、注入人味。当用户说"人语化"、"去AI味"、"润色"、"让这更像人写的"、"人性化处理"时自动激活。支持小说、文章、文案等多种文本类型。
---

# 人语化处理

将 AI 生成的文本转化为更自然、更像人类写作风格的内容。

## 路由规则

根据用户输入类型，路由到不同处理器：

| 输入类型 | 示例 | 路由目标 |
|---------|------|----------|
| 纯文本 | `/humanize-text [文本内容]` | `skills/humanize-text/SKILL.md`（直接处理） |
| 自检评分 | `/humanize-text 自检 [文本]` | `skills/humanize-text/SKILL.md`（自检模式） |
| 文件路径 | `/humanize-text ./我的小说/` | `agents/humanize-text.md`（文件处理器） |
| 路径+章节 | `/humanize-text ./我的小说/ 第3-5章` | `agents/humanize-text.md`（文件处理器） |
| 仅章节号 | `/humanize-text 第3章` | `agents/humanize-text.md`（当前目录查找） |

### 判断逻辑

```
输入包含路径（./、/、相对路径）→ 调用 agent
输入包含"第X章"、"chapter"等关键词 → 调用 agent
输入包含"自检"关键词 → 调用 skill（自检模式）
输入是纯文本 → 调用 skill（直接处理）
```

## 为什么需要人语化？

| AI 特征 | 人类特征 |
|--------|----------|
| 中性、精致、过于平衡 | 个人语气、情感、主观偏见 |
| 句式整齐划一 | 长短句交替，节奏变化 |
| 安全词选择、公式化模式 | 创意跃迁、幽默、不可预测 |
| 喜欢升华主题 | 留白、余韵、不完美的真实 |

## 使用方式

```
/humanize-text [待处理的文本]

# 指定场景
/humanize-text 场景:小说对话 [文本]
/humanize-text 场景:小红书 [文本]
/humanize-text 场景:邮件 [文本]
/humanize-text 场景:学术论文 [文本]

# 指定程度
/humanize-text 程度:轻度 [文本]   # 保留大部分原文，微调
/humanize-text 程度:中度 [文本]   # 平衡改写
/humanize-text 程度:深度 [文本]   # 大幅重构

# 自检评分
/humanize-text 自检 [文本]       # AI程度检测评分

# 文件模式
/humanize-text ./我的小说/                    # 交互式选择章节
/humanize-text ./我的小说/ 第3章              # 处理指定章节
/humanize-text ./我的小说/ 第3-5章            # 处理章节范围
/humanize-text ./我的小说/ 全部               # 处理所有章节
```

## 核心指标

### 1. 困惑度 (Perplexity)

```
❌ AI: "我非常喜欢阅读，因为书籍是人类进步的阶梯。"
✅ 人类: "书这玩意儿，那是我的精神鸦片。"
```

### 2. 爆发度 (Burstiness)

```
❌ AI: 虽然天气很冷，但是我们依然坚持工作，因为这对项目很重要。
✅ 人类: 冷死。但还得干。没办法，项目要死人了。
```

## 禁止词汇清单

- 学术装X系：深入探讨、领域、旨在、致力于、多维度、底层逻辑
- 废话系：综上所述、毋庸置疑、值得注意的是、至关重要
- 幻觉系：织锦、交响曲、灯塔、画卷、星辰大海、踔厉奋发

## 相关命令

| 需求 | 使用 |
|------|------|
| 综合质量检查 | `/quality-check [文本]` |
| 流水账检测 | `/boring-detect [文本]` |
| 开篇检查 | `/opening-check [文本]` |

## 相关资源

- 纯文本处理知识库：`skills/humanize-text/SKILL.md`
- 文件处理器（并行子代理）：`agents/humanize-text.md`
- 24种AI模式详解：`skills/humanize-text/references/ai-patterns.md`
