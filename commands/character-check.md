---
description: 角色质量检查工具，检测人设扁平化、前后不统一、配角工具人化等问题。当用户说"角色检查"、"人设检查"、"人物检查"、"检查角色"时自动激活。
---

# 角色质量检查

检测小说中角色相关的常见问题，包括人设扁平化、前后不统一、配角工具人化、视角杂乱。

## 路由规则

根据用户输入类型，路由到不同处理器：

| 输入类型 | 示例 | 路由目标 |
|---------|------|----------|
| 纯文本 | `/character-check [文本内容]` | `skills/character-check/SKILL.md`（直接检查） |
| 文件路径 | `/character-check ./我的小说/` | `agents/character-check.md`（文件处理器） |
| 路径+章节 | `/character-check ./我的小说/ 第3-5章` | `agents/character-check.md`（文件处理器） |
| 仅章节号 | `/character-check 第3章` | `agents/character-check.md`（当前目录查找） |
| 配合设定 | `/character-check --设定 [人物宝典路径] ./我的小说/` | `agents/character-check.md`（文件处理器+设定对照） |

### 判断逻辑

```
输入包含路径（./、/、相对路径）→ 调用 agent
输入包含"第X章"、"chapter"等关键词 → 调用 agent
输入是纯文本 → 调用 skill（直接检查）
```

## 检查维度

| 维度 | 核心问题 |
|------|----------|
| 人设扁平化 | 所有角色说话风格一样，分不清是谁在说话 |
| 人设一致性 | 角色行为与之前设定的性格矛盾 |
| 配角工具人化 | 配角只为主角服务，没有自己的生活和动机 |
| 视角问题 | 同一段落内频繁切换视角，读者会混乱 |

## 评分标准

| 等级 | 分数 | 描述 | 建议 |
|------|------|------|------|
| 优秀 | 80-100 | 角色鲜明，个性突出 | 保持即可 |
| 良好 | 60-79 | 有个性但可加强 | 针对性优化 |
| 及格 | 40-59 | 存在明显问题 | 需要改写 |
| 不及格 | 0-39 | 严重角色问题 | 需要重构 |

## 使用方式

```
/character-check [文本内容]

# 指定检查项
/character-check --扁平化 [文本]        # 只检查人设扁平化
/character-check --一致性 [文本]        # 只检查人设一致性
/character-check --配角 [文本]          # 只检查配角工具人化
/character-check --视角 [文本]          # 只检查视角问题

# 配合人物设定
/character-check --设定 [人物宝典路径] [文本]

# 文件模式
/character-check ./我的小说/                    # 交互式选择章节
/character-check ./我的小说/ 第3章              # 检查指定章节
/character-check ./我的小说/ 第3-5章            # 检查章节范围
/character-check ./我的小说/ 全部               # 检查所有章节
```

## 一句话自检

```
遮住角色名字，你能分辨出是谁在说话吗？
如果不看设定，角色的行为符合你的印象吗？
配角不出场的时候，他在做什么？
```

## 相关命令

| 需求 | 使用 |
|------|------|
| 综合质量检查 | `/quality-check [文本]` |
| 创意与选题检查 | `/concept-check [文本]` |
| 人语化处理 | `/humanize-text [文本]` |

## 相关资源

- 核心知识库：`skills/character-check/SKILL.md`
- 文件处理器（并行子代理）：`agents/character-check.md`
- 检查维度详解：`skills/character-check/references/check-dimensions.md`
- 报告模板：`skills/character-check/references/report-template.md`
