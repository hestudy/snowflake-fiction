# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

Snowflake Fiction 是一个 Claude Code 插件，提供完整的小说创作工具链。包含核心技能：

| 技能 | 用途 | 触发词 |
|------|------|--------|
| snowflake-fiction | 雪花写作法创作小说（编排器） | 写小说、创作故事、雪花法 |
| outline-concept | 故事构思（步骤1→1.5c→2构思期，含写作风格配置） | 构思故事、验证创意、故事概念、帮我想一个故事 |
| character-design | 角色设计（步骤3→5→7人物深化链） | 角色设计、人物设计、新增角色、深化角色 |
| scene-plan | 场景规划（步骤8→9场景设计链） | 场景规划、规划场景、场景设计、场景清单、规划章节 |
| chapter-write | 创作期续写（步骤10，支持批量生成） | 续写、写章节、生成章节、写下一章、批量生成、继续写、写正文 |
| novel-review | 小说质量复核检查 | 小说复核、章节检查、一致性检查、质量检查 |
| humanize-text | AI文本人语化处理（24种检测模式+灵魂注入，支持指定路径和章节） | 人语化、去AI味、润色 |
| quality-check | 内容质量评估（冲突/情绪/期待感/节奏/钩子五维打分） | 质量检查、内容检查、综合评估、检查质量、小说质量 |
| character-check | 角色质量检查（扁平化/一致性/工具人/视角四维检测） | 角色检查、人设检查、人物检查、检查角色 |
| boring-detect | 流水账专项检测（无冲突/无情绪/无期待感/信息堆砌四维检测） | 流水账检测、检查流水账、平淡检测、流水账 |
| concept-check | 创意与选题检查（题材匹配/辨识度/书名质量/混搭/世界观五维检测） | 选题检查、创意检查、题材检查、检查选题、书名检查 |
| opening-check | 开篇质量检查（黄金三章法则，支持文件模式） | 开篇检查、黄金三章、检查开篇、检查前三章 |
| novel-export | 导出各平台格式 | 导出小说、番茄格式、起点格式 |

## 目录结构

```
snowflake-fiction/
├── .claude-plugin/
│   ├── plugin.json           # 插件元数据
│   └── marketplace.json      # Marketplace 发布配置
├── agents/
│   ├── outline-builder.md    # 大纲构建 agent（步骤4+6）
│   ├── snowflake-fiction.md  # 雪花写作法文件处理器（目录扫描+批量生成）
│   ├── chapter-write.md      # 创作期续写文件处理器（并行子代理架构）
│   ├── humanize-text.md      # 人语化文件处理器（并行子代理架构）
│   ├── novel-review.md       # 小说复核文件处理器（分批子代理架构）
│   ├── novel-export.md       # 格式导出文件处理器（并行子代理架构）
│   ├── quality-check.md      # 内容质量评估文件处理器（并行子代理架构）
│   ├── character-check.md    # 角色质量检查文件处理器（并行子代理架构）
│   ├── concept-check.md      # 创意与选题检查文件处理器（并行子代理架构）
│   ├── opening-check.md      # 开篇质量检查文件处理器（并行子代理架构）
│   └── boring-detect.md      # 流水账检测文件处理器（并行子代理架构）
├── skills/
│   ├── snowflake-fiction/    # 雪花写作法主技能
│   │   ├── SKILL.md          # 核心编排知识库（工作流程+委托规则）
│   │   └── references/       # 参考模板
│   │       ├── step-prompts.md              # 每步提示词
│   │       ├── character-template.md        # 人物卡片模板
│   │       ├── scene-template.md            # 场景规划模板
│   │       ├── export-format.md             # 导出格式说明
│   │       ├── long-novel-guide.md          # 长篇小说指南
│   │       └── million-word-webnovel-guide.md # 百万级网文指南
│   ├── novel-review/         # 小说复核技能
│   │   ├── SKILL.md          # 核心知识库（检查维度+报告格式）
│   │   └── references/
│   │       ├── consistency-check-prompt.md  # 一致性检查提示词
│   │       ├── character-state-template.md  # 角色状态追踪
│   │       ├── timeline-template.md         # 时间线追踪
│   │       ├── foreshadowing-tracker.md     # 伏笔追踪
│   │       └── review-report-template.md    # 复核报告模板
│   ├── character-design/     # 角色设计技能（步骤3+5+7）
│   │   └── SKILL.md
│   ├── character-check/      # 角色质量检查技能
│   │   ├── SKILL.md          # 核心知识库（检查维度+输出格式）
│   │   └── references/
│   │       ├── check-dimensions.md        # 四维度检测标准和修复示例
│   │       └── report-template.md         # 单章/批量报告模板
│   ├── scene-plan/           # 场景规划技能（步骤8+9）
│   │   └── SKILL.md
│   ├── chapter-write/        # 创作期续写技能（步骤10）
│   │   ├── SKILL.md          # 核心知识库（单章生成+流水账自检）
│   │   └── references/
│   │       └── writing-guide.md           # 写作提示词、检查清单、钩子设计
│   ├── opening-check/        # 开篇质量检查技能
│   │   ├── SKILL.md          # 核心知识库（黄金三章法则+输出格式）
│   │   └── references/
│   │       ├── golden-three-chapters.md   # 黄金三章法则详解和检查清单
│   │       ├── common-problems.md         # 常见开篇问题诊断和修复示例
│   │       └── report-template.md         # 单章/批量报告模板
│   ├── concept-check/        # 创意与选题检查技能
│   │   ├── SKILL.md          # 核心知识库（检查维度+输出格式）
│   │   └── references/
│   │       ├── check-dimensions.md        # 五维度检测标准和示例
│   │       ├── optimization-formulas.md   # 辨识度优化公式和改写示范
│   │       ├── book-title-guide.md        # 书名质量指南（7种起名思路+案例）
│   │       └── report-template.md         # 单章/批量报告模板
│   ├── quality-check/        # 内容质量评估技能
│   │   ├── SKILL.md          # 核心知识库（评估维度+输出格式）
│   │   └── references/
│   │       ├── evaluation-dimensions.md   # 五维度评分标准和检查清单
│   │       └── report-template.md         # 单章/批量报告模板
│   ├── humanize-text/        # 人语化处理技能
│   │   ├── SKILL.md          # 核心知识库（纯文本处理）
│   │   └── references/
│   │       ├── ai-patterns.md           # 24种AI写作模式详解
│   │       ├── soul-injection.md        # 灵魂注入技巧
│   │       ├── scene-modes.md           # 5种场景化处理模式
│   │       └── banned-words.md          # 禁止词汇清单
│   ├── boring-detect/        # 流水账检测技能
│   │   ├── SKILL.md          # 核心知识库（检测维度+输出格式）
│   │   └── references/
│   │       ├── detection-dimensions.md  # 四维度检测标准和示例
│   │       ├── fix-formulas.md          # 修复公式和改写示范
│   │       └── report-template.md       # 单章/批量报告模板
│   └── novel-export/         # 格式导出技能
│       ├── SKILL.md          # 核心知识库（格式转换规则）
│       └── references/
│           ├── platform-rules.md         # 各平台转换规则和示例
│           └── naming-convention.md      # 输出目录命名规范
└── README.md                 # 使用文档
```

## 技能架构

### snowflake-fiction（雪花写作法）

采用 Command / Skill / Agent 三层架构：

- **Command**（`commands/snowflake-fiction.md`）：用户入口，根据输入类型路由到 Skill 或 Agent
- **Skill**（`skills/snowflake-fiction/SKILL.md`）：核心编排知识库，定义工作流程和各步骤委托规则
- **Agent**（`agents/snowflake-fiction.md`）：文件处理器，扫描目录、判断进度、批量生成章节

支持三种模式：
- **短篇小说**（1-3万字）：12步流程
- **长篇小说**（10-50万字）：15步流程，多卷结构
- **百万级网文**（100万字+）：商业节奏设计，黄金三章、付费卡点、爽点密度

流程阶段：构思期（含写作风格配置） → 设计期 → 构建期 → 规划期 → 创作期 → 润色期 → 导出期

Agent 层负责：目录扫描和进度判断、从任意步骤恢复创作、批量章节生成的并行子代理派发（默认并发2）、进度报告。

输出目录规则：直接在当前工作目录下创建 `[小说名]/`（不再创建 `novel-output/` 中间层）；向后兼容已有的 `novel-output/[小说名]/` 结构

小说项目目录包含 `00-写作风格.md` 写作风格配置文件（构思期步骤1.5c生成），章节生成时自动读取。支持8种快捷预设（沙雕搞笑/热血燃向/虐心催泪/甜宠治愈/冷硬写实/文青诗意/暗黑压抑/轻松日常），可微调参数，可粘贴风格示例锚文。

### character-design（角色设计）

覆盖步骤3→5→7的人物深化链，可独立使用，也可被 snowflake-fiction 主流程调用。

- **步骤3**：一页纸人物卡片（核心设定、人物弧光、标志性元素）
- **步骤5**：人物背景故事（童年创伤、成长经历、性格形成根源）
- **步骤7**：人物宝典（七大分类的完整角色资料库）

支持三种模式：快速卡片（仅步骤3）、完整深化（步骤3→5→7）、局部更新（更新已有角色）

触发词：角色设计、人物设计、新增角色、深化角色、完善人物

### scene-plan（场景规划）

覆盖步骤8→9的场景设计链，可独立使用，也可被 snowflake-fiction 主流程调用。

- **步骤8**：场景清单（将大纲拆解为结构化场景列表，含冲突类型和节奏检查）
- **步骤9**：场景详细规划（每个场景的三要素展开，主动/被动模板）

支持三种模式：全量规划（步骤8→9）、局部规划（指定章节重跑）、仅生成清单（步骤8）

局部重跑时只更新指定章节文件，不影响其他章节的已有规划。

触发词：场景规划、规划场景、场景设计、场景清单、规划章节

### chapter-write（创作期续写）

采用 Command / Skill / Agent 三层架构：

- **Command**（`commands/chapter-write.md`）：用户入口，所有输入路由到 Agent
- **Skill**（`skills/chapter-write/SKILL.md`）：核心知识库，定义单章生成流程和流水账自检规则
- **Agent**（`agents/chapter-write.md`）：文件处理器，扫描目录、章节范围解析、并行子代理派发

覆盖步骤10的正文生成，可独立使用，也可被 snowflake-fiction 主流程调用。

核心特性：
- 批次间顺序、批次内并行（确保第N章能读到第N-1章）
- 前置检查：缺少场景规划的章节跳过并报告
- 续写模式：自动定位最后一章编号
- 每章生成后自动执行流水账自检（冲突/情绪/期待感/节奏 4维度）
- 开篇强化：第1-3章额外检查黄金三章标准
- 写作风格注入：自动读取 `00-写作风格.md`，按配置参数控制叙事视角、情绪基调、对话密度等

并发策略：默认并发2，推荐范围1-3。

知识库拆分为1个 references 文件：writing-guide.md（写作提示词、检查清单、钩子设计、风格参数注入规则）。

触发词：续写、写章节、生成章节、写下一章、批量生成、继续写、写正文

### outline-builder（大纲构建 agent）

覆盖步骤4（一页纸大纲）和步骤6（四页纸完整大纲），是构建期的核心汇聚节点。

与 skill 的区别：agent 会**自主读取**项目目录中的所有已有文件（概念文件、人物卡片、背景故事），无需用户手动提供内容，综合生成逻辑自洽的大纲。

- **步骤4**：将五句式大纲扩展为一页纸大纲（400-600字，含场景/对话/情绪）
- **步骤6**：综合所有材料生成四页纸完整大纲（2000-3000字，含章节规划/伏笔清单/灾难事件标注）

支持：`--rebuild`（忽略已有大纲重新生成）、`--step4-only`（只生成一页纸大纲）

生成后自动执行一致性检查（人物行为、时间线、三幕结构、伏笔自洽）。

触发词：生成大纲、构建大纲、写大纲、大纲重建、重新生成大纲

### novel-review（小说复核）

采用 Command / Skill / Agent 三层架构：

- **Command**（`commands/novel-review.md`）：用户入口，根据输入类型路由到 Skill 或 Agent
- **Skill**（`skills/novel-review/SKILL.md`）：核心知识库，定义检查维度、评判标准和报告格式
- **Agent**（`agents/novel-review.md`）：文件处理器，扫描目录、分批派发子代理执行检查、汇总报告

**核心挑战**：长篇小说可能有数十万字，一次性加载所有内容会导致上下文溢出。

**解决方案**：Agent 层使用子代理架构，将检查任务拆分为独立的小任务，分批执行（每批最多2个并行）。

检查项目：
- 角色一致性：性格、对话、能力、关系
- 时间线：时间流逝、季节、年龄
- 设定一致性：能力体系、物品、地点、规则
- 大纲偏离：核心事件、支线、节奏
- 伏笔回收：埋设、回收、超期预警
- 文风一致性：视角、语言风格、AI痕迹

知识库拆分为5个 references 文件：consistency-check-prompt.md（提示词模板）、character-state-template.md（角色状态）、timeline-template.md（时间线）、foreshadowing-tracker.md（伏笔追踪）、review-report-template.md（报告模板）。

输出目录规则：在小说目录下创建 `review/` 子目录，包含追踪文件和报告

### humanize-text（人语化处理）

采用 Command / Skill / Agent 三层架构：

- **Command**（`commands/humanize-text.md`）：用户入口，根据输入类型路由到 Skill 或 Agent
- **Skill**（`skills/humanize-text/SKILL.md`）：核心知识库，处理纯文本和自检评分
- **Agent**（`agents/humanize-text.md`）：文件处理器，扫描目录、并行派发子代理逐章处理

基于 Wikipedia "Signs of AI writing" 指南，检测并修复 24 种 AI 写作模式，同时注入灵魂（观点、节奏、复杂情绪、第一人称）。

知识库拆分为4个 references 文件：ai-patterns.md（24种模式）、soul-injection.md（灵魂注入）、scene-modes.md（场景模式）、banned-words.md（禁止词汇）。

支持场景：小说对话、小红书、学术论文、商务邮件

文件模式：指定小说目录路径 + 章节范围，Agent 自动扫描目录、并行派发子代理（最多3个并发）逐章处理并直接回写。

### quality-check（内容质量评估）

采用 Command / Skill / Agent 三层架构：

- **Command**（`commands/quality-check.md`）：用户入口，根据输入类型路由到 Skill 或 Agent
- **Skill**（`skills/quality-check/SKILL.md`）：核心知识库，定义评估维度和输出格式
- **Agent**（`agents/quality-check.md`）：文件处理器，扫描目录、并行派发子代理逐章评估、汇总报告

从五个维度评估文本内容吸引力，定位问题段落，给出优先修改建议。

- **冲突强度**（25%）：是否有明确冲突，是否足够强烈
- **情绪密度**（25%）：角色情绪是否饱满，读者能否共情
- **期待感**（20%）：读者是否想继续看下去
- **节奏控制**（15%）：张弛是否得当
- **钩子设计**（15%）：开头是否抓人，结尾是否有悬念

知识库拆分为2个 references 文件：evaluation-dimensions.md（五维度评分标准和检查清单）、report-template.md（单章/批量报告模板）。

不负责 AI 痕迹检测（→ humanize-text）和流水账检测（→ boring-detect）。

文件模式：指定小说目录路径 + 章节范围，Agent 自动扫描目录、并行派发子代理（最多3个并发）逐章评估，汇总报告写入 `review/quality-report.md`。

触发词：质量检查、内容检查、综合评估、检查质量、小说质量

### character-check（角色质量检查）

采用 Command / Skill / Agent 三层架构：

- **Command**（`commands/character-check.md`）：用户入口，根据输入类型路由到 Skill 或 Agent
- **Skill**（`skills/character-check/SKILL.md`）：核心知识库，定义检查维度和输出格式
- **Agent**（`agents/character-check.md`）：文件处理器，扫描目录、并行派发子代理逐章检查、汇总报告

从四个维度检测角色质量问题：

- **人设扁平化**（30%）：所有角色说话风格一样，分不清是谁
- **人设一致性**（30%）：角色行为与设定矛盾
- **配角工具人化**（25%）：配角只为主角服务，无独立人格
- **视角问题**（15%）：频繁切换视角导致混乱

知识库拆分为2个 references 文件：check-dimensions.md（四维度检测标准和修复示例）、report-template.md（单章/批量报告模板）。

文件模式：指定小说目录路径 + 章节范围，Agent 自动扫描目录、并行派发子代理（最多3个并发）逐章检查，汇总报告写入 `review/character-report.md`。

触发词：角色检查、人设检查、人物检查、检查角色

### boring-detect（流水账检测）

采用 Command / Skill / Agent 三层架构：

- **Command**（`commands/boring-detect.md`）：用户入口，根据输入类型路由到 Skill 或 Agent
- **Skill**（`skills/boring-detect/SKILL.md`）：核心知识库，定义检测维度和输出格式
- **Agent**（`agents/boring-detect.md`）：文件处理器，扫描目录、并行派发子代理逐章检测、汇总报告

从四个维度检测流水账问题：

- **无冲突**（30%）：只有事件罗列，没有矛盾碰撞
- **无情绪**（25%）：只有动作描述，缺少角色情感反应
- **无期待感**（25%）：读者不想知道接下来发生什么
- **信息堆砌**（20%）：大量灌输设定和背景

知识库拆分为3个 references 文件：detection-dimensions.md（四维度检测标准和示例）、fix-formulas.md（修复公式和改写示范）、report-template.md（单章/批量报告模板）。

文件模式：指定小说目录路径 + 章节范围，Agent 自动扫描目录、并行派发子代理（最多3个并发）逐章检测，汇总报告写入 `review/boring-report.md`。

触发词：流水账检测、检查流水账、平淡检测、流水账

### concept-check（创意与选题检查）

采用 Command / Skill / Agent 三层架构：

- **Command**（`commands/concept-check.md`）：用户入口，根据输入类型路由到 Skill 或 Agent
- **Skill**（`skills/concept-check/SKILL.md`）：核心知识库，定义检查维度和输出格式
- **Agent**（`agents/concept-check.md`）：文件处理器，扫描目录、并行派发子代理逐章检测、汇总报告

从五个维度检测选题质量问题：

- **题材匹配**（25%）：标签与实际内容是否匹配
- **辨识度**（25%）：是否有独特卖点，与同类作品的差异
- **书名质量**（20%）：书名是否吸引人、贴合内容、有记忆点
- **混搭合理性**（15%）：元素数量、主次分明、逻辑自洽
- **世界观设定**（15%）：设定数量、呈现方式、渐进展开

知识库拆分为4个 references 文件：check-dimensions.md（五维度检测标准和示例）、optimization-formulas.md（辨识度优化公式和改写示范）、book-title-guide.md（书名质量指南、7种起名思路、男女频案例）、report-template.md（单章/批量报告模板）。

文件模式：指定小说目录路径 + 章节范围，Agent 自动扫描目录、并行派发子代理（最多3个并发）逐章检测，汇总报告写入 `review/concept-report.md`。

触发词：选题检查、创意检查、题材检查、检查选题、书名检查

### opening-check（开篇质量检查）

采用 Command / Skill / Agent 三层架构：

- **Command**（`commands/opening-check.md`）：用户入口，根据输入类型路由到 Skill 或 Agent
- **Skill**（`skills/opening-check/SKILL.md`）：核心知识库，定义黄金三章法则和输出格式
- **Agent**（`agents/opening-check.md`）：文件处理器，扫描目录、定位前三章、并行派发子代理逐章检查

基于"黄金三章"法则检查小说开篇质量：

- **第一章**（40分）：3秒抓眼球，前300字有爆点（危机/金手指/反转）
- **第二章**（30分）：强化冲突，紧迫目标+具体阻碍
- **第三章**（30分）：爽点反馈，小胜利+结尾钩子

知识库拆分为3个 references 文件：golden-three-chapters.md（黄金三章法则详解和检查清单）、common-problems.md（常见开篇问题诊断和修复示例）、report-template.md（单章/批量报告模板）。

文件模式：指定小说目录路径，Agent 自动扫描目录、定位前三章、并行派发子代理（最多3个并发）逐章检查，汇总报告写入 `review/opening-report.md`。

触发词：开篇检查、黄金三章、检查开篇、检查前三章

### novel-export（格式导出）

采用 Command / Skill / Agent 三层架构：

- **Command**（`commands/novel-export.md`）：用户入口，根据输入类型路由到 Skill 或 Agent
- **Skill**（`skills/novel-export/SKILL.md`）：核心知识库，定义格式转换规则和输出格式
- **Agent**（`agents/novel-export.md`）：文件处理器，扫描目录、并行派发子代理逐章导出

支持平台：番茄小说、起点中文网、晋江文学城、知乎盐选、七猫小说、通用纯文本、Word

知识库拆分为2个 references 文件：platform-rules.md（各平台转换规则和示例）、naming-convention.md（输出目录命名规范）。

关键格式差异：
- 番茄：无缩进，回车分段，无空行
- 起点：首行缩进2字符（全角空格）

文件模式：指定小说目录路径 + 章节范围，Agent 自动扫描目录、并行派发子代理（最多3个并发）逐章导出并写入 `导出/[平台名]/` 目录。

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
