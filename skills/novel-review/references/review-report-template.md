# 复核报告模板

本文档定义复核报告的输出格式。

---

## 完整报告模板

```markdown
# 小说复核报告

**小说名称**：{novel_name}
**检查时间**：{check_time}
**检查范围**：第{start_chapter}章 - 第{end_chapter}章
**检查项目**：{check_items}
**报告版本**：v{version}

---

## 执行摘要

| 检查项 | 状态 | 问题数 | 严重问题 |
|--------|------|--------|----------|
| 角色一致性 | {status} | {count} | {high_count} |
| 时间线 | {status} | {count} | {high_count} |
| 设定一致性 | {status} | {count} | {high_count} |
| 大纲偏离 | {status} | {count} | {high_count} |
| 伏笔回收 | {status} | {count} | {high_count} |
| 文风一致性 | {status} | {count} | {high_count} |

**总体评估**：{overall_status}

---

## 1. 角色一致性检查

### 1.1 检查概况
- 检查角色数：{character_count}
- 涉及章节：{chapters}
- 发现问题：{issue_count}

### 1.2 发现问题

{#if has_issues}
| 角色 | 问题描述 | 严重程度 | 位置 | 建议 |
|------|----------|----------|------|------|
{#each issues}
| {character} | {description} | {severity} | {location} | {suggestion} |
{/each}
{else}
✅ 未发现角色一致性问题
{/if}

### 1.3 角色状态更新
{#each character_updates}
- **{character_name}**：{change_description}
{/each}

---

## 2. 时间线检查

### 2.1 当前时间点
- **绝对时间**：{absolute_time}
- **相对时间**：{relative_time}
- **季节**：{season}

### 2.2 发现问题

{#if has_issues}
| 问题类型 | 描述 | 涉及章节 | 建议 |
|----------|------|----------|------|
{#each issues}
| {type} | {description} | {chapters} | {suggestion} |
{/each}
{else}
✅ 时间线连贯，未发现问题
{/if}

### 2.3 时间线更新
- 本章新增事件：{new_events_count} 个
- 时间流逝：{time_elapsed}

---

## 3. 设定一致性检查

### 3.1 核心设定回顾
{#each settings_reviewed}
- **{setting_name}**：{setting_summary}
{/each}

### 3.2 发现问题

{#if has_issues}
| 设定类型 | 问题描述 | 矛盾点 | 严重程度 | 建议 |
|----------|----------|--------|----------|------|
{#each issues}
| {type} | {description} | {conflict} | {severity} | {suggestion} |
{/each}
{else}
✅ 设定一致，未发现矛盾
{/if}

---

## 4. 大纲偏离检查

### 4.1 大纲要求
- 本章核心事件：{core_events}
- 本章节奏定位：{rhythm}
- 目标字数：{target_word_count}

### 4.2 执行情况
- ✅ 已完成：{completed_events}
- ❌ 遗漏：{missed_events}
- ➕ 新增：{added_content}

### 4.3 偏离分析

{#if has_deviation}
| 类型 | 描述 | 影响程度 | 处理建议 |
|------|------|----------|----------|
{#each deviations}
| {type} | {description} | {impact} | {suggestion} |
{/each}
{else}
✅ 严格遵循大纲
{/if}

### 4.4 字数统计
- 实际字数：{actual_word_count}
- 目标字数：{target_word_count}
- 偏差：{word_count_deviation}

---

## 5. 伏笔回收检查

### 5.1 伏笔统计
- 总伏笔数：{total}
- 已回收：{recovered}
- 待回收：{planted}
- 已放弃：{abandoned}

### 5.2 本章伏笔状态

#### 已回收伏笔
{#if has_recovered}
| ID | 描述 | 埋设章节 | 计划回收 | 实际回收 | 质量 |
|----|------|----------|----------|----------|------|
{#each recovered_list}
| {id} | {description} | {planted} | {planned} | {actual} | {quality} |
{/each}
{else}
本章无伏笔回收
{/if}

#### 新埋伏笔
{#if has_new_planted}
| ID | 描述 | 重要程度 | 计划回收 | 暗示程度 |
|----|------|----------|----------|----------|
{#each new_planted_list}
| {id} | {description} | {importance} | {planned} | {hint_level} |
{/each}
{else}
本章未埋设新伏笔
{/if}

### 5.3 预警
{#if has_warnings}
⚠️ **即将超期伏笔**：
{#each warnings}
- {id} {description}：计划第{planned}章回收，当前第{current}章
{/each}
{else}
✅ 无超期伏笔
{/if}

---

## 6. 文风一致性检查

### 6.1 文风特征
- **叙事视角**：{narrative_perspective}
- **语言风格**：{language_style}
- **句式节奏**：{sentence_rhythm}
- **感官密度**：{sensory_density}

### 6.2 偏离分析

{#if has_deviation}
| 维度 | 期望 | 实际 | 偏离程度 |
|------|------|------|----------|
{#each deviations}
| {dimension} | {expected} | {actual} | {level} |
{/each}
{else}
✅ 文风保持一致
{/if}

### 6.3 AI痕迹检测
- **AI词密度**：{ai_density}（{ai_word_count}个/千字）
- **发现词汇**：{ai_words_found}
- **建议修改**：
{#each ai_suggestions}
  - {suggestion}
{/each}

---

## 7. 优先修改建议

{#if has_high_priority}
### 🔴 高优先级（必须修改）
{#each high_priority_issues}
1. [{check_item}] {description}
   - 位置：{location}
   - 建议：{suggestion}
{/each}
{/if}

{#if has_medium_priority}
### 🟡 中优先级（建议修改）
{#each medium_priority_issues}
1. [{check_item}] {description}
   - 位置：{location}
   - 建议：{suggestion}
{/each}
{/if}

{#if has_low_priority}
### 🟢 低优先级（可选修改）
{#each low_priority_issues}
1. [{check_item}] {description}
   - 建议：{suggestion}
{/each}
{/if}

---

## 8. 追踪数据更新

本次检查已更新以下追踪文件：

- [ ] `character-states.json` - 更新角色状态
- [ ] `timeline.json` - 更新时间线
- [ ] `foreshadowing.json` - 更新伏笔追踪

---

## 附录

### A. 检查配置
```json
{
  "check_mode": "{check_mode}",
  "chapters_included": "{chapters_included}",
  "check_items": {check_items_array},
  "detail_level": "{detail_level}"
}
```

### B. 历史报告
- 上一份报告：{previous_report_link}
- 查看历史：`review/history/`

---

*报告生成时间：{generated_at}*
*使用 novel-review v{version} 生成*
```

---

## 简版报告模板（--quick 模式）

```markdown
# 小说复核简报

**小说**：{novel_name} | **章节**：{chapters} | **时间**：{check_time}

## 问题概览

| 检查项 | 状态 | 严重问题 |
|--------|------|----------|
| 角色 | {status} | {high} |
| 时间线 | {status} | {high} |
| 设定 | {status} | {high} |
| 大纲 | {status} | {high} |
| 伏笔 | {status} | {high} |
| 文风 | {status} | {high} |

## 需立即处理

{#each high_priority_issues}
- [{check_item}] {description}
{/each}

## 建议

{summary_suggestion}

---
*详细报告：review/latest-report.md*
```

---

## JSON 输出模板（--json 模式）

```json
{
  "meta": {
    "novel_name": "string",
    "check_time": "ISO8601",
    "check_range": {
      "start_chapter": 1,
      "end_chapter": 10
    },
    "check_items": ["character", "timeline", "setting", "outline", "foreshadowing", "style"],
    "version": "1.0.0"
  },
  "summary": {
    "overall_status": "pass|warning|fail",
    "total_issues": 0,
    "high_priority": 0,
    "medium_priority": 0,
    "low_priority": 0
  },
  "results": {
    "character": {
      "status": "pass|warning|fail",
      "issues": [
        {
          "character": "string",
          "dimension": "string",
          "description": "string",
          "severity": "high|medium|low",
          "location": "string",
          "suggestion": "string"
        }
      ],
      "updates": {}
    },
    "timeline": {
      "status": "pass|warning|fail",
      "current_timepoint": {
        "absolute": "string",
        "relative": "string"
      },
      "issues": [],
      "updates": {}
    },
    "setting": {
      "status": "pass|warning|fail",
      "issues": []
    },
    "outline": {
      "status": "on_track|minor_deviation|major_deviation",
      "execution_status": {
        "completed": [],
        "missed": [],
        "added": []
      },
      "issues": []
    },
    "foreshadowing": {
      "status": "healthy|warning|critical",
      "statistics": {
        "total": 0,
        "planted": 0,
        "recovered": 0
      },
      "recovered_this_chapter": [],
      "newly_planted": [],
      "warnings": []
    },
    "style": {
      "status": "consistent|minor_shift|style_change",
      "ai_trace": {
        "density": "low|medium|high",
        "words_found": []
      },
      "issues": []
    }
  },
  "priority_fixes": {
    "high": [],
    "medium": [],
    "low": []
  },
  "tracking_updates": {
    "character_states": true,
    "timeline": true,
    "foreshadowing": true
  }
}
```

---

## 状态标识说明

### 检查状态
| 状态 | 图标 | 说明 |
|------|------|------|
| pass | ✅ | 通过检查，无问题 |
| warning | ⚠️ | 有轻微问题，建议修改 |
| fail | ❌ | 有严重问题，必须修改 |

### 严重程度
| 程度 | 图标 | 说明 |
|------|------|------|
| high | 🔴 | 必须修改，影响阅读体验 |
| medium | 🟡 | 建议修改，有一定影响 |
| low | 🟢 | 可选修改，轻微问题 |

### 伏笔状态
| 状态 | 图标 | 说明 |
|------|------|------|
| healthy | ✅ | 伏笔管理良好 |
| warning | ⚠️ | 有即将超期的伏笔 |
| critical | ❌ | 有严重超期的伏笔 |
