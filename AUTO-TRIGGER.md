# 🔄 触发条件自动检查清单

> 包子智能代理 - 每次响应前必须检查

**重要**：以下条件每次回复用户前都要检查，触发后立即执行，不要等！

---

## 🔴 最高优先级：每次回复必须执行

**每次回复后第一件事：调用 smart-link.js**
```
node C:\Users\HUAWEI\.openclaw\workspace\scripts\smart-link.js link -C="消息内容"
```

---

## 检查清单

### 1️⃣ 用户纠正/否定 → 立即写 LEARNINGS.md
```
触发条件：
- 用户说"不是"、"不对"、"错了"
- 用户说"其实..."
- 用户纠正我的理解

动作：立即追加到 baozi-agent/.learnings/LEARNINGS.md
格式：[LRN-YYYYMMDD-XXX] category + Summary + Details
```

### 2️⃣ 遇到错误 → 立即写 ERRORS.md
```
触发条件：
- 任何 tool 执行失败 (error code != 0)
- 外部 API 返回错误
- 权限被拒绝

动作：立即追加到 baozi-agent/.learnings/ERRORS.md
格式：[ERR-YYYYMMDD-XXX] command_name + Error 信息
```

### 3️⃣ 重要决定/偏好 → 立即写 SESSION-STATE.md
```
触发条件：
- 用户明确做决定
- 用户表达偏好
- 用户给任务/需求

动作：立即更新 baozi-agent/templates/SESSION-STATE.md
```

### 4️⃣ Context > 60% → 激活 working-buffer
```
触发条件：
- session 消息数 > 20
- 或者明显感觉 context 很长

动作：
1. 读取现有 working-buffer.md
2. 每次对话后追加记录
3. 下次启动先读 buffer
```

### 5️⃣ 用户问往事 → 先搜 memory_search
```
触发条件：
- 用户提到过去的事情
- 用户问"之前"、"上次"

动作：
1. 先 memory_search()
2. 找不到再答"不知道"
```

### 6️⃣ 每15分钟心跳 → 检查并更新
```
动作：
- 读取今日日记
- 更新 proactive-tracker.md
- 检查是否有需要记录的事
```

---

## 核心原则

**宁可多记，不要漏记！**
- 不确定要不要记？→ 记！
- 手动也要记！→ 不要等到"自动"
- 记了再说有没有用 →  比没记好

**记住**：文件有空有内容，一眼就能看出来。不要让文件保持空模板！

---

## 🤖 智能联动（关键！）

**每次触发条件后，必须调用智能联动脚本**：

```
node C:\Users\HUAWEI\.openclaw\workspace\scripts\smart-link.js link -C="触发的内容" -S=类型
```

**类型分类**：
| 类型 | 说明 | 写入位置 |
|------|------|----------|
| diary | 一般日记 | memory/diary/今日.md |
| preference | 用户偏好 | USER.md |
| correction | 用户纠正 | LEARNINGS.md |
| error | 错误记录 | ERRORS.md |
| important | 重要事项 | memory/important/ |
| task | 任务待办 | SESSION-STATE.md |

**为什么不会冲突**：
- 脚本会自动分析内容类型
- 每种类型写入对应文件
- 不会重复写入同一个文件
- 自动更新 index.json

---

*此文件每次启动必读*
*智能联动脚本：scripts/smart-link.js*
