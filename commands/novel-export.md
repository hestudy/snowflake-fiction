---
description: 将小说文本转换为各平台投稿格式。当用户说"导出小说"、"转换为平台格式"、"番茄格式"、"起点格式"、"投稿格式"时自动激活。支持番茄小说、起点中文网、晋江文学城、知乎盐选等主流平台。
---

# 小说导出格式转换

将 Markdown 或纯文本转换为各大小说平台的投稿格式。

## 路由规则

根据用户输入类型，路由到不同处理器：

| 输入类型 | 示例 | 路由目标 |
|---------|------|----------|
| 纯文本 | `/novel-export 番茄 [文本内容]` | `skills/novel-export/SKILL.md`（直接转换） |
| 文件路径 | `/novel-export 番茄 ./我的小说/` | `agents/novel-export.md`（文件处理器） |
| 路径+章节 | `/novel-export 番茄 ./我的小说/ 第3-5章` | `agents/novel-export.md`（文件处理器） |
| 批量模式 | `/novel-export 番茄 ./正文/ --batch` | `agents/novel-export.md`（文件处理器） |
| 仅章节号 | `/novel-export 番茄 第3章` | `agents/novel-export.md`（当前目录查找） |

### 判断逻辑

```
输入包含路径（./、/、相对路径）→ 调用 agent
输入包含"第X章"、"chapter"等关键词 → 调用 agent
输入包含 --batch 标志 → 调用 agent
输入是纯文本 → 调用 skill（直接转换）
```

## 支持的平台

| 平台 | 格式 | 特点 |
|------|------|------|
| **番茄小说** | 纯文本 | 无缩进，回车分段，无空行 |
| **起点中文网** | 纯文本 | 首行缩进2字符 |
| **晋江文学城** | 纯文本 | 遵循晋江规范 |
| **知乎盐选** | 在线编辑 | 短篇2-5万字 |
| **七猫小说** | 纯文本 | 类似番茄 |
| **通用纯文本** | txt | 2字符缩进，章节间空行 |
| **Word 文档** | docx | 保留基本格式 |

## 使用方式

```bash
# 纯文本转换（→ Skill）
/novel-export 番茄 [文本内容]
/novel-export 起点 [文本内容]

# 文件模式（→ Agent）
/novel-export 番茄 ./我的小说/正文/
/novel-export 番茄 ./我的小说/ 第3-5章
/novel-export 起点 ./正文/ --batch
/novel-export 起点 ./正文/ --batch --concurrency 5
```

## 快捷指令

```
/番茄格式 [文本]    # 同 /novel-export 番茄
/起点格式 [文本]    # 同 /novel-export 起点
/晋江格式 [文本]    # 同 /novel-export 晋江
```

## 并发控制

| 参数 | 说明 |
|------|------|
| `--batch` | 启用批量转换模式 |
| `--concurrency N` | 并发数量，默认 **3**，推荐 2-5 |

## 相关命令

| 需求 | 使用 |
|------|------|
| 人语化处理 | `/humanize-text [路径]` |
| 综合质量检查 | `/quality-check [文本]` |
| 小说复核 | `/novel-review [路径]` |

## 相关资源

- 核心知识库：`skills/novel-export/SKILL.md`
- 文件处理器（并行子代理）：`agents/novel-export.md`
- 平台转换规则：`skills/novel-export/references/platform-rules.md`
- 命名规范：`skills/novel-export/references/naming-convention.md`
