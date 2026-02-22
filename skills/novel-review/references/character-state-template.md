# 角色状态追踪模板

本文档定义角色状态的记录格式，用于跨章节追踪角色变化。

---

## JSON 数据结构

```json
{
  "version": "1.0",
  "last_updated": "2024-03-15T10:30:00Z",
  "novel_name": "小说名称",
  "characters": {
    "[角色ID]": {
      "basic_info": {
        "name": "角色名",
        "aliases": ["别名1", "别名2"],
        "role": "主角|反派|配角|路人",
        "importance": "main|major|minor"
      },
      "attributes": {
        "age": 25,
        "gender": "男|女|其他",
        "occupation": "职业",
        "appearance": "外貌描述关键词"
      },
      "characteristics": {
        "personality": ["性格关键词1", "性格关键词2"],
        "speech_style": "对话风格描述",
        "catchphrases": ["口头禅1", "口头禅2"],
        "habits": ["习惯动作1", "习惯动作2"]
      },
      "abilities": {
        "level": "当前等级",
        "level_system": "所属能力体系",
        "skills": ["技能1", "技能2"],
        "items": ["持有物品1", "持有物品2"]
      },
      "relationships": {
        "[其他角色ID]": {
          "type": "朋友|敌人|师徒|恋人|家人",
          "status": "当前关系状态",
          "development": "关系发展历程摘要"
        }
      },
      "history": {
        "first_appearance": "第X章",
        "key_events": [
          {
            "chapter": "第X章",
            "event": "关键事件描述",
            "impact": "对角色的影响"
          }
        ]
      },
      "current_state": {
        "as_of_chapter": "第X章",
        "location": "当前所在地点",
        "status": "正常|受伤|失踪|死亡",
        "mental_state": "心理状态描述",
        "recent_changes": ["最近的变化"]
      }
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
  "characters": {
    "MC001": {
      "basic_info": {
        "name": "林晨",
        "aliases": ["晨哥", "林总"],
        "role": "主角",
        "importance": "main"
      },
      "attributes": {
        "age": 35,
        "gender": "男",
        "occupation": "企业家/投资人",
        "appearance": "普通相貌，眼镜，短发"
      },
      "characteristics": {
        "personality": ["沉稳", "果断", "略带腹黑"],
        "speech_style": "简洁有力，偶尔冷幽默",
        "catchphrases": ["有意思", "按计划行事"],
        "habits": ["思考时扶眼镜", "重要决定前深呼吸"]
      },
      "abilities": {
        "level": "商界新贵",
        "level_system": "财富等级",
        "skills": ["投资眼光", "商业谈判", "信息整合"],
        "items": ["重生前的记忆", "第一桶金500万"]
      },
      "relationships": {
        "SUP001": {
          "type": "恋人",
          "status": "追求中",
          "development": "前世错过，今生重新追求"
        },
        "ANT001": {
          "type": "敌人",
          "status": "暗中对抗",
          "development": "前世害死自己的人，今生复仇对象"
        }
      },
      "history": {
        "first_appearance": "第1章",
        "key_events": [
          {
            "chapter": "第1章",
            "event": "重生回2010年大学宿舍",
            "impact": "获得前世记忆，决心改变命运"
          },
          {
            "chapter": "第2章",
            "event": "彩票中奖500万",
            "impact": "获得启动资金"
          }
        ]
      },
      "current_state": {
        "as_of_chapter": "第20章",
        "location": "北京",
        "status": "正常",
        "mental_state": "野心勃勃，复仇计划稳步推进",
        "recent_changes": ["成立投资公司", "与苏婉关系升温"]
      }
    },
    "SUP001": {
      "basic_info": {
        "name": "苏婉",
        "aliases": ["婉儿"],
        "role": "女主",
        "importance": "main"
      },
      "attributes": {
        "age": 22,
        "gender": "女",
        "occupation": "大学生/校花",
        "appearance": "清秀脱俗，长发，气质出众"
      },
      "characteristics": {
        "personality": ["温柔", "聪明", "外柔内刚"],
        "speech_style": "轻声细语，偶尔小傲娇",
        "catchphrases": ["讨厌", "你猜"],
        "habits": ["紧张时咬嘴唇", "开心时眼睛弯成月牙"]
      },
      "abilities": {
        "level": "普通人",
        "level_system": "财富等级",
        "skills": ["学习能力", "人际交往"],
        "items": []
      },
      "relationships": {
        "MC001": {
          "type": "恋人",
          "status": "暧昧期",
          "development": "从同学到互有好感"
        }
      },
      "history": {
        "first_appearance": "第1章",
        "key_events": [
          {
            "chapter": "第5章",
            "event": "与林晨重逢",
            "impact": "开始新的缘分"
          }
        ]
      },
      "current_state": {
        "as_of_chapter": "第20章",
        "location": "北京",
        "status": "正常",
        "mental_state": "对林晨有好感但有些困惑",
        "recent_changes": ["接受了林晨的第一次约会"]
      }
    },
    "ANT001": {
      "basic_info": {
        "name": "王志远",
        "aliases": ["王少"],
        "role": "反派",
        "importance": "major"
      },
      "attributes": {
        "age": 28,
        "gender": "男",
        "occupation": "富二代",
        "appearance": "英俊但带阴鸷"
      },
      "characteristics": {
        "personality": ["阴险", "自负", "睚眦必报"],
        "speech_style": "表面客气，暗藏锋芒",
        "catchphrases": ["有意思", "走着瞧"],
        "habits": ["冷笑", "把玩打火机"]
      },
      "abilities": {
        "level": "富二代",
        "level_system": "财富等级",
        "skills": ["人脉", "阴谋"],
        "items": ["王家背景"]
      },
      "relationships": {
        "MC001": {
          "type": "敌人",
          "status": "暗中敌对",
          "development": "尚未正面冲突，但已开始关注林晨"
        }
      },
      "history": {
        "first_appearance": "第3章",
        "key_events": []
      },
      "current_state": {
        "as_of_chapter": "第20章",
        "location": "北京",
        "status": "正常",
        "mental_state": "开始注意到林晨这个变量",
        "recent_changes": []
      }
    }
  }
}
```

---

## 使用说明

### 初始化
在第一次运行 `novel-review` 时，系统会：
1. 读取 `人物卡片/` 和 `人物宝典/` 目录
2. 自动生成初始的角色状态文件
3. 保存到 `review/character-states.json`

### 更新规则
每次检查新章节时：
1. 读取当前状态文件
2. 检查章节中的角色变化
3. 更新 `current_state` 和 `history`
4. 保存更新后的文件

### 手动编辑
可以手动编辑此文件来：
- 添加遗漏的角色
- 修正错误的状态
- 补充关系网络

### 版本管理
建议在每卷结束时：
1. 备份当前状态文件到 `review/history/`
2. 清理不活跃角色的信息（保留基本信息）
3. 开始新卷的状态追踪

---

## 字段说明

### importance（重要程度）
- `main`：主要角色，需要详细追踪
- `major`：重要配角，需要追踪关键变化
- `minor`：次要角色，只需记录基本信息

### status（状态）
- `正常`：角色正常活动
- `受伤`：角色受伤，影响行动
- `失踪`：角色下落不明
- `死亡`：角色已死亡

### relationship.type（关系类型）
- `朋友`：普通朋友
- `敌人`：敌对关系
- `师徒`：师徒关系
- `恋人`：恋爱关系
- `家人`：家人关系
- `同事`：工作关系
- `暧昧`：暧昧关系
- `前任`：前任关系
