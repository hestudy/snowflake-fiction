---
description: 创作期续写工具，逐章或批量生成小说正文。当用户说"续写"、"写章节"、"生成章节"、"写下一章"、"批量生成"、"继续写"、"写正文"时自动激活。
---

# 创作期续写

基于场景规划逐章生成小说正文，支持单章续写和批量生成。

## 路由规则

所有输入类型均路由到 agent 处理：

| 输入类型 | 示例 | 路由目标 |
|---------|------|----------|
| 无输入 | `/chapter-write` | `agents/chapter-write.md`（扫描目录，自动续写下一章） |
| 文件路径 | `/chapter-write ./我的小说/` | `agents/chapter-write.md`（扫描目录） |
| 指定章节 | `/chapter-write 第5章` | `agents/chapter-write.md`（生成指定章节） |
| 章节范围 | `/chapter-write 第5-10章` | `agents/chapter-write.md`（批量生成） |
| 续写N章 | `/chapter-write 今天2章` | `agents/chapter-write.md`（从最后一章续写） |
| 路径+章节 | `/chapter-write ./我的小说/ 第3-5章` | `agents/chapter-write.md`（指定目录+范围） |

### 判断逻辑

```
所有输入 → 调用 chapter-write agent
```

本命令不路由到 skill 层。agent 内部读取 skill 知识库获取写作规则。

## 使用方式

```
/chapter-write                                    # 自动续写下一章
/chapter-write 第5章                              # 生成指定章节
/chapter-write 第5-10章                           # 批量生成章节范围
/chapter-write 今天3章                            # 从最后一章续写3章
/chapter-write ./我的小说/ 第3-5章                # 指定目录+章节范围
/chapter-write --concurrency 3                    # 自定义并发数
```

## 推荐工作流

```
1. /chapter-write [章节范围]
2. 根据生成结果决定：
   ├── 满意 → /quality-check 快速检查
   ├── 需要调整 → 手动修改后继续
   └── 批量生成 → /chapter-write 今天N章
3. /humanize-text [正文]
4. /novel-export [平台]
```

## 相关命令

| 需求 | 使用 |
|------|------|
| 完整创作流程 | `/snowflake-fiction` |
| 质量检查 | `/quality-check [文本]` |
| 流水账检测 | `/boring-detect [文本]` |
| 人语化处理 | `/humanize-text [文本]` |
| 导出格式 | `/novel-export [平台]` |

## 相关资源

- 核心知识库：`skills/chapter-write/SKILL.md`
- 文件处理器（并行子代理）：`agents/chapter-write.md`
- 写作提示词与检查清单：`skills/chapter-write/references/writing-guide.md`
