# Snowflake Fiction - 小说创作工具套件

Claude Code 插件，提供完整的小说创作工具链。

## 功能模块

### 1. snowflake-fiction - 雪花写作法

使用雪花写作法(Snowflake Method)系统化创作小说。

**触发词**：写小说、创作故事、雪花法、帮我构思一个故事

**功能**：
- 短篇小说模式（1-3万字）：12步完成
- 长篇小说模式（10万字+）：15步完成，多卷结构
- 从一句话概括到完整正文的完整流程

### 2. humanize-text - 人语化处理

将AI生成的文本进行人语化处理，去除机器味、注入人味。

**触发词**：人语化、去AI味、润色、让这更像人写的、人性化处理

**功能**：
- 全面人语化
- 对话优化
- 小红书风格
- 学术降重
- 邮件润色

### 3. novel-export - 小说导出

将小说文本转换为各平台投稿格式。

**触发词**：导出小说、转换为平台格式、番茄格式、起点格式、投稿格式

**支持平台**：
- 番茄小说
- 起点中文网
- 晋江文学城
- 知乎盐选
- 七猫小说
- 通用纯文本

## 推荐工作流

```
snowflake-fiction → humanize-text → novel-export
     (创作)           (润色)          (导出)
```

## 安装

将此目录作为 Claude Code 插件使用：

1. 复制到 `~/.claude/plugins/` 目录
2. 或在项目目录中直接使用

## 目录结构

```
snowflake-fiction/
├── .claude-plugin/
│   └── plugin.json        # 插件元数据
├── skills/
│   ├── humanize-text/
│   │   └── SKILL.md       # 人语化技能
│   ├── novel-export/
│   │   └── SKILL.md       # 导出技能
│   └── snowflake-fiction/
│       ├── SKILL.md       # 雪花写作法主技能
│       └── references/    # 参考模板
│           ├── step-prompts.md
│           ├── character-template.md
│           ├── scene-template.md
│           ├── export-format.md
│           └── long-novel-guide.md
└── README.md
```

## License

MIT
