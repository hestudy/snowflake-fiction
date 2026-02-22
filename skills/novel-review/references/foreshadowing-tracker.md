# 伏笔追踪模板

本文档定义伏笔的记录格式，用于管理伏笔的埋设与回收。

---

## JSON 数据结构

```json
{
  "version": "1.0",
  "last_updated": "2024-03-15T10:30:00Z",
  "novel_name": "小说名称",
  "next_id": 12,
  "foreshadowings": [
    {
      "id": "F001",
      "description": "伏笔描述",
      "type": "main|sub|detail",
      "status": "planted|recovered|abandoned",
      "planted": {
        "chapter": "第3章",
        "content": "埋伏笔的具体内容",
        "hint_level": "obvious|balanced|subtle"
      },
      "planned_recovery": {
        "chapter": "第15章",
        "method": "计划回收方式"
      },
      "actual_recovery": {
        "chapter": "第15章",
        "content": "实际回收内容",
        "quality": "excellent|good|poor"
      },
      "tags": ["角色", "物品", "事件"],
      "notes": "备注"
    }
  ],
  "statistics": {
    "total": 10,
    "planted": 5,
    "recovered": 4,
    "abandoned": 1,
    "overdue": 0
  }
}
```

---

## 示例数据

```json
{
  "version": "1.0",
  "last_updated": "2024-03-15T10:30:00Z",
  "novel_name": "重生2010",
  "next_id": 12,
  "foreshadowings": [
    {
      "id": "F001",
      "description": "林晨前世死亡真相",
      "type": "main",
      "status": "recovered",
      "planted": {
        "chapter": "第1章",
        "content": "林晨站在天台边缘，回忆起被推下的那一刻",
        "hint_level": "obvious"
      },
      "planned_recovery": {
        "chapter": "第10章",
        "method": "通过调查发现幕后黑手"
      },
      "actual_recovery": {
        "chapter": "第10章",
        "content": "林晨查到前世推他的人是王志远",
        "quality": "good"
      },
      "tags": ["核心", "复仇"],
      "notes": "主线伏笔，推动整个故事"
    },
    {
      "id": "F002",
      "description": "苏婉的家族背景",
      "type": "sub",
      "status": "recovered",
      "planted": {
        "chapter": "第5章",
        "content": "苏婉接到电话，脸色微变",
        "hint_level": "subtle"
      },
      "planned_recovery": {
        "chapter": "第20章",
        "method": "苏婉被迫回家，揭示身份"
      },
      "actual_recovery": {
        "chapter": "第18章",
        "content": "苏婉是某大家族的千金",
        "quality": "excellent"
      },
      "tags": ["角色", "爱情线"],
      "notes": "提前回收，增加剧情张力"
    },
    {
      "id": "F003",
      "description": "神秘投资人",
      "type": "sub",
      "status": "planted",
      "planted": {
        "chapter": "第12章",
        "content": "有人在暗中收购林晨看中的公司股票",
        "hint_level": "balanced"
      },
      "planned_recovery": {
        "chapter": "第25章",
        "method": "揭露投资人的身份"
      },
      "actual_recovery": null,
      "tags": ["商战", "悬疑"],
      "notes": "计划在第25章揭露"
    },
    {
      "id": "F004",
      "description": "林晨的前世未婚妻",
      "type": "main",
      "status": "planted",
      "planted": {
        "chapter": "第8章",
        "content": "林晨梦到前世的女人模糊面孔",
        "hint_level": "subtle"
      },
      "planned_recovery": {
        "chapter": "第30章",
        "method": "这个女人出现，引发情感冲突"
      },
      "actual_recovery": null,
      "tags": ["核心", "情感"],
      "notes": "将在后期引发林晨与苏婉的危机"
    },
    {
      "id": "F005",
      "description": "彩票站的神秘老人",
      "type": "detail",
      "status": "abandoned",
      "planted": {
        "chapter": "第2章",
        "content": "彩票站有个看报纸的老人，意味深长地看了林晨一眼",
        "hint_level": "subtle"
      },
      "planned_recovery": {
        "chapter": "第15章",
        "method": "老人再次出现，揭示身份"
      },
      "actual_recovery": null,
      "tags": ["细节"],
      "notes": "剧情调整后决定放弃此支线"
    },
    {
      "id": "F006",
      "description": "王志远的秘密项目",
      "type": "main",
      "status": "planted",
      "planted": {
        "chapter": "第15章",
        "content": "王志远接到电话谈论一个'代号X'的项目",
        "hint_level": "balanced"
      },
      "planned_recovery": {
        "chapter": "第40章",
        "method": "项目曝光，成为林晨反击的机会"
      },
      "actual_recovery": null,
      "tags": ["商战", "复仇"],
      "notes": "远期伏笔，与主线复仇相关"
    }
  ],
  "statistics": {
    "total": 6,
    "planted": 3,
    "recovered": 2,
    "abandoned": 1,
    "overdue": 0
  }
}
```

---

## 伏笔分类说明

### type（伏笔类型）
| 类型 | 说明 | 必须回收 | 示例 |
|------|------|----------|------|
| `main` | 主线伏笔 | 是 | 主角身世、核心谜团 |
| `sub` | 支线伏笔 | 建议 | 配角秘密、次级事件 |
| `detail` | 细节伏笔 | 可选 | 暗示、氛围渲染 |

### hint_level（暗示程度）
| 程度 | 说明 | 效果 |
|------|------|------|
| `obvious` | 明显 | 读者能猜到，期待验证 |
| `balanced` | 适中 | 有迹可循但需要思考 |
| `subtle` | 隐晦 | 回收时恍然大悟 |

### status（伏笔状态）
| 状态 | 说明 | 后续处理 |
|------|------|----------|
| `planted` | 已埋未收 | 等待回收 |
| `recovered` | 已回收 | 完成 |
| `abandoned` | 已放弃 | 不再追踪 |

### quality（回收质量）
| 等级 | 说明 |
|------|------|
| `excellent` | 超出预期，有惊喜感 |
| `good` | 符合预期，合理回收 |
| `poor` | 生硬牵强，读者不满 |

---

## 伏笔管理规则

### 埋设规则
1. 主线伏笔数量控制在 3-5 条
2. 支线伏笔数量控制在 5-10 条
3. 同一时期活跃伏笔不超过 10 条
4. 避免过于隐晦或过于明显

### 回收规则
1. 主线伏笔必须在故事结束前回收
2. 支线伏笔建议在 20 章内回收
3. 回收前至少要有 1 次以上的暗示/提醒
4. 避免一次性回收大量伏笔（信息过载）

### 超期预警
- 伏笔超过计划回收章节 3 章以内：低风险
- 伏笔超过计划回收章节 5 章：中等风险，需要提醒
- 伏笔超过计划回收章节 10 章以上：高风险，需要处理

### 放弃处理
如果决定放弃某条伏笔：
1. 更新状态为 `abandoned`
2. 在 notes 中记录放弃原因
3. 考虑是否需要在正文中做轻微处理（避免读者困惑）

---

## 使用说明

### 新伏笔识别
当检查章节发现新伏笔时：
1. 分配新 ID（使用 `next_id`）
2. 填写基本信息
3. 设置计划回收章节
4. 更新 `next_id`

### 伏笔回收确认
当检查章节发现伏笔回收时：
1. 找到对应伏笔
2. 更新状态为 `recovered`
3. 填写实际回收信息
4. 评估回收质量

### 周期检查
建议每 10 章进行一次伏笔检查：
1. 统计各状态数量
2. 识别超期伏笔
3. 调整回收计划

---

## 常见问题

### Q: 如何判断一个伏笔是否过于隐晦？
A: 如果伏笔在回收时读者完全没有印象，可能过于隐晦。建议在回收前增加一次"提醒"。

### Q: 伏笔太多怎么办？
A: 优先回收主线伏笔，支线伏笔可以适当放弃，细节伏笔可以忽略。

### Q: 伏笔回收失败怎么办？
A: 如果回收质量为 `poor`，建议：
1. 在后续章节补充铺垫
2. 或者重新设计回收方式
3. 极端情况下可以"软重启"（用新事件覆盖）

### Q: 如何避免伏笔忘记？
A:
1. 使用本追踪系统
2. 每次写作前查看当前活跃伏笔
3. 在大纲中标注伏笔位置
