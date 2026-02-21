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

### 方式一：通过 Marketplace 安装（推荐）

```bash
# 添加 marketplace
/plugin marketplace add hestudy/snowflake-fiction

# 安装插件
/plugin install snowflake-fiction@snowflake-fiction
```

### 方式二：从 GitHub 仓库克隆

```bash
# 克隆到 Claude Code 插件目录
git clone https://github.com/hestudy/snowflake-fiction.git \
  ~/.claude/plugins/marketplaces/snowflake-fiction
```

### 方式三：从本地目录安装

```bash
# 如果你已经克隆了仓库
cp -r /path/to/snowflake-fiction ~/.claude/plugins/marketplaces/
```

### 方式四：项目级安装

将此仓库作为子模块添加到你的项目中：

```bash
git submodule add https://github.com/hestudy/snowflake-fiction.git .claude/plugins/snowflake-fiction
```

### 启用插件

在 `~/.claude/settings.json` 中添加：

```json
{
  "enabledPlugins": {
    "snowflake-fiction": true
  }
}
```

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
