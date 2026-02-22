# 时间线追踪模板

本文档定义时间线的记录格式，用于跨章节追踪时间流逝。

---

## JSON 数据结构

```json
{
  "version": "1.0",
  "last_updated": "2024-03-15T10:30:00Z",
  "novel_name": "小说名称",
  "timeline_config": {
    "start_date": "2010-09-01",
    "date_format": "absolute|relative",
    "time_system": "现实|虚构纪年"
  },
  "current_state": {
    "absolute_time": "2010-09-20",
    "relative_time": "故事开始后第20天",
    "current_chapter": "第10章",
    "season": "秋季",
    "weather": "晴"
  },
  "events": [
    {
      "id": "E001",
      "chapter": "第1章",
      "time": {
        "absolute": "2010-09-01",
        "relative": "故事开始"
      },
      "event": "事件描述",
      "participants": ["角色1", "角色2"],
      "location": "地点",
      "significance": "high|medium|low"
    }
  ],
  "time_markers": [
    {
      "chapter": "第1章",
      "markers": [
        {
          "type": "absolute|relative|environment",
          "text": "原文中的时间标记",
          "parsed": "解析后的时间"
        }
      ]
    }
  ],
  "character_ages": {
    "[角色ID]": {
      "name": "角色名",
      "birth_date": "1988-05-15",
      "age_at_start": 22,
      "current_age": 22,
      "age_last_updated": "第10章"
    }
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
  "timeline_config": {
    "start_date": "2010-09-01",
    "date_format": "absolute",
    "time_system": "现实"
  },
  "current_state": {
    "absolute_time": "2010-10-15",
    "relative_time": "故事开始后第45天",
    "current_chapter": "第20章",
    "season": "秋季",
    "weather": "秋高气爽"
  },
  "events": [
    {
      "id": "E001",
      "chapter": "第1章",
      "time": {
        "absolute": "2010-09-01",
        "relative": "故事开始"
      },
      "event": "林晨重生回2010年大学宿舍",
      "participants": ["林晨"],
      "location": "北京大学宿舍",
      "significance": "high"
    },
    {
      "id": "E002",
      "chapter": "第2章",
      "time": {
        "absolute": "2010-09-02",
        "relative": "第2天"
      },
      "event": "林晨购买彩票",
      "participants": ["林晨"],
      "location": "彩票站",
      "significance": "medium"
    },
    {
      "id": "E003",
      "chapter": "第3章",
      "time": {
        "absolute": "2010-09-05",
        "relative": "第5天"
      },
      "event": "林晨彩票中奖500万",
      "participants": ["林晨"],
      "location": "彩票中心",
      "significance": "high"
    },
    {
      "id": "E004",
      "chapter": "第5章",
      "time": {
        "absolute": "2010-09-10",
        "relative": "第10天"
      },
      "event": "林晨与苏婉重逢",
      "participants": ["林晨", "苏婉"],
      "location": "校园",
      "significance": "high"
    },
    {
      "id": "E005",
      "chapter": "第10章",
      "time": {
        "absolute": "2010-09-25",
        "relative": "第25天"
      },
      "event": "林晨注册投资公司",
      "participants": ["林晨"],
      "location": "工商局",
      "significance": "medium"
    },
    {
      "id": "E006",
      "chapter": "第15章",
      "time": {
        "absolute": "2010-10-01",
        "relative": "第31天"
      },
      "event": "林晨与苏婉第一次约会",
      "participants": ["林晨", "苏婉"],
      "location": "北京某餐厅",
      "significance": "medium"
    }
  ],
  "time_markers": [
    {
      "chapter": "第1章",
      "markers": [
        {
          "type": "absolute",
          "text": "2010年9月1日",
          "parsed": "2010-09-01"
        },
        {
          "type": "environment",
          "text": "初秋的阳光透过窗户",
          "parsed": "秋季"
        }
      ]
    },
    {
      "chapter": "第2章",
      "markers": [
        {
          "type": "relative",
          "text": "第二天一早",
          "parsed": "+1天"
        }
      ]
    },
    {
      "chapter": "第15章",
      "markers": [
        {
          "type": "absolute",
          "text": "国庆节",
          "parsed": "2010-10-01"
        }
      ]
    }
  ],
  "character_ages": {
    "MC001": {
      "name": "林晨",
      "birth_date": "1988-03-15",
      "age_at_start": 22,
      "current_age": 22,
      "age_last_updated": "第20章"
    },
    "SUP001": {
      "name": "苏婉",
      "birth_date": "1988-07-20",
      "age_at_start": 22,
      "current_age": 22,
      "age_last_updated": "第20章"
    }
  }
}
```

---

## 时间标记识别规则

### 绝对时间标记
| 类型 | 示例 | 解析 |
|------|------|------|
| 完整日期 | 2010年9月1日 | 2010-09-01 |
| 年月 | 2010年9月 | 2010-09 |
| 节日 | 国庆节 | 根据年份推断具体日期 |
| 节气 | 立秋 | 根据年份推断具体日期 |
| 年份 | 2010年 | 2010 |

### 相对时间标记
| 类型 | 示例 | 解析 |
|------|------|------|
| 天数 | 三天后、第5天 | +3天、+5天 |
| 周数 | 一周后、半个月后 | +7天、+15天 |
| 月数 | 两个月后 | +2月 |
| 年数 | 三年后 | +3年 |
| 顺序 | 第二天、翌日 | +1天 |
| 事件锚点 | 师父死后的第三天 | 相对于特定事件 |

### 环境时间标记
| 类型 | 示例 | 解析 |
|------|------|------|
| 时段 | 清晨、傍晚、深夜 | 时间段 |
| 季节 | 炎炎夏日、秋高气爽 | 季节信息 |
| 天气 | 雨过天晴、大雪纷飞 | 天气+季节 |
| 服饰 | 穿着棉袄 | 暗示冬季 |
| 活动 | 蝉鸣阵阵、梅花盛开 | 季节暗示 |

---

## 时间线冲突检测规则

### 时间跳跃检测
- 如果两章之间时间跳跃超过3天，且没有任何说明，标记为警告
- 如果时间跳跃超过1个月，需要检查是否有遗漏的过渡

### 季节冲突检测
- 检查季节描述是否与时间线匹配
- 例如：9月不能描写"春暖花开"

### 年龄冲突检测
- 检查角色年龄是否随时间正确增长
- 生日是否在正确的时间点

### 顺序冲突检测
- 检查事件的因果关系是否与时间顺序一致
- 例如：不能"明天"见到"昨天"才认识的人

---

## 使用说明

### 初始化
1. 确定故事开始的绝对时间（如2010-09-01）
2. 确定使用的时间系统（现实/虚构纪年）
3. 创建初始时间线文件

### 更新规则
1. 每检查一章，提取时间标记
2. 计算新的当前时间
3. 添加新的事件记录
4. 更新角色年龄（如有变化）

### 时间跳跃处理
如果检测到时间跳跃：
1. 在报告中标注
2. 建议添加过渡说明
3. 记录跳跃前后的状态变化

---

## 字段说明

### significance（事件重要性）
- `high`：关键事件，影响主线
- `medium`：重要事件，影响支线或角色发展
- `low`：普通事件，时间节点标记

### date_format（日期格式）
- `absolute`：使用具体日期（如2010-09-01）
- `relative`：使用相对时间（如第5天）
- `mixed`：混合使用

### time_system（时间系统）
- `现实`：使用现实世界的日历
- `虚构纪年`：使用虚构的纪年方式（如"修仙历352年"）
