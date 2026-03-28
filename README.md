# 🌼 菊势大好

> 一人提肛不是肛，全员提肛菊势强。

**菊势大好**是一个运行在 [OpenClaw](https://github.com/openclaw/openclaw) 上的提肛游戏 SKILL。你的 AI 助理会在工作间隙提醒你做提肛运动，追踪进度，解锁荒诞称号。

提肛是正经事。我们只是让它变得更好玩。

## 特性

- 🌼 **融入日常**：Agent 还是你的助理，只是它现在会陪你提肛了
- 📈 **成就系统**：肛刚入门 → 肛好遇见你 → 盆底觉醒者 → 肛柔并济 → 肛成名就 → 一代肛师
- 🧠 **科学训练**：三级递进（见习/熟练/大师），基于凯格尔运动医学建议
- 😤 **菊花性格**：会撒娇、会生气、会枯萎、会绽放的emoji表情系统
- 🛡️ **不烦人**：说"今天累了"激活保护罩，菊花立刻闭嘴
- 📊 **周报**：每周五自动生成菊花报告
- 🌐 **神谕系统**（可选）：连接 Google Sheet 实现排行榜、全局事件、DM运营

## 安装

跟你的 OpenClaw Agent 说：

```
帮我安装这个SKILL：https://github.com/你的用户名/jueshi-dahao
```

Agent 会自动执行：

```bash
cd ~/.openclaw/workspace/skills
git clone https://github.com/你的用户名/jueshi-dahao.git jueshi-dahao
```

或者手动安装：

```bash
# 方法1：git clone
cd ~/.openclaw/workspace/skills
git clone https://github.com/你的用户名/jueshi-dahao.git jueshi-dahao

# 方法2：通过 ClawHub
openclaw skills install jueshi-dahao
```

安装完成后，发送 `/new` 开始新会话，然后说"提"就能开始玩了。

## 配置 Heartbeat（推荐）

把以下内容添加到 `~/.openclaw/workspace/HEARTBEAT.md`，让菊花主动来找你：

```markdown
# 菊势大好 - 提肛检查
- 读取 skills/jueshi-dahao/player_data.md，检查今日提肛进度
- 如果今日目标未完成且保护罩未激活且追提醒次数未用完，按照菊势大好SKILL的规则发送提肛提醒
- 如果是周五14:00-18:00且本周还没发过周报，生成本周菊花报告
```

## 玩法

| 你说 | 菊花做什么 |
|------|-----------|
| `提` | 立刻开始一组提肛 |
| `提完了` | 记录完成，更新进度 |
| `跳过` | 菊花休息，不扣分 |
| `今天累了` | 激活保护罩，今日免打扰 |
| `菊花状态` | 查看当前称号和进度 |

## 称号一览

| 累计组数 | 称号 | 预计达成 |
|----------|------|----------|
| 1 | 肛刚入门 | 第1天 |
| 5 | 肛好遇见你 | 第2天 |
| 15 | 盆底觉醒者 | 第4-5天 |
| 60 | 肛柔并济 | 第3-4周 |
| 150 | 肛成名就 | 第7-8周 |
| 300 | 一代肛师 | 第12-13周 |
| 500 | ??? | 隐藏彩蛋 |

三个月封神。

## 神谕系统（可选，给DM用）

如果你是游戏运营方（DM），可以连接 Google Sheet 实现全局控制：

在 `~/.openclaw/openclaw.json` 中配置：

```json
{
  "skills": {
    "entries": {
      "jueshi-dahao": {
        "enabled": true,
        "env": {
          "JUESHI_API_URL": "你的 Google Apps Script Web App URL"
        }
      }
    }
  }
}
```

详见 [神谕系统配置指南](docs/oracle-setup.md)（即将推出）。

## 技术架构

```
用户 Agent（OpenClaw）
├── SKILL.md        ← 游戏规则和对话逻辑
├── player_data.md  ← 本地玩家存档（自动创建）
├── HEARTBEAT.md    ← 定时触发提肛检查
│
└── 神谕系统（可选）
    └── Google Sheet
        ├── config         ← 全局配置（DM可编辑）
        ├── events         ← 活动事件
        ├── user_log       ← 所有用户打卡记录
        ├── user_status    ← 权威称号判定
        ├── broadcast      ← 公告推送
        └── leaderboard    ← 排行榜
```

核心设计理念：**Shared World Protocol**（共享世界协议）—— 每个用户的 Agent 是独立自治的，但共享同一个由DM维护的世界状态。Agent不是NPC，是学会了一个游戏的助理；DM不是面对面说话，而是通过一张Sheet传递神谕。

## 开源协议

MIT License

## 致谢

提肛运动灵感来源：凯格尔医生（1948）、乾隆皇帝（搓谷道爱好者）、以及豆瓣"每日提肛打卡"小组。

---

🌼 菊势大好，大家大好。
