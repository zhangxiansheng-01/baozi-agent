# Learnings Log

Captured learnings, corrections, and discoveries. Review before major tasks.

---

## [LRN-20260309-001] memory-system-failure
**Priority**: critical
**Status**: resolved
### Summary
记忆系统文件都是空模板，没有实际内容记录 Details
- LE
###ARNINGS.md, ERRORS.md, SESSION-STATE.md 都只有模板格式
- 用户纠正"需要把包子智能代理放workspace"时没有记录
- 对话内容没有写入 working-buffer
- 原因：知道规则但没有真正执行触发条件
### Suggested Action
- 建立每次启动时检查模板是否工作的机制
- 用户纠正/重要决定时立即记录
- 错误发生时立即记录

## [LRN-20260309-004] 测试联动-用户纠正
**Priority**: low
**Status**: testing
### Summary
测试：用户说"你理解错了！"
### Details
- 触发条件：用户纠正
- 验证：是否能自动联动到其他文件
- 预期：自动更新 outcome-journal + index + tags

---

## [LRN-20260309-005] 智能联动系统集成完成
**Priority**: high
**Status**: resolved
### Summary
创建 smart-link.js 智能归类脚本，完美集成所有记忆文件
### Details
- 问题：之前手动同步会冲突、重复
- 解决：创建 smart-link.js 自动分类脚本
- 测试：已验证 7 种类型都能正确归类不冲突
### Implementation
- scripts/smart-link.js - 智能归类脚本
- 更新 SKILL.md - 加入智能联动说明
- 更新 LINKAGE.md - 加入分类规则
- 更新 AUTO-TRIGGER.md - 加入调用说明
### Key Points
- 每种类型对应唯一目标文件，不会冲突
- 自动更新 index.json
- 脚本位置: scripts/smart-link.js

---

## [LRN-20260309-003] auto-trigger-system
**Priority**: critical
**Status**: resolved
### Summary
创建自动触发检查清单，解决手动记录不生效问题
### Details
- 问题：触发条件写在 SKILL.md 但没有自动执行
- 用户建议：写代码让它们联动起来
- 解决：创建 AUTO-TRIGGER.md 检查清单
- 更新 SKILL.md 加入触发执行流程
### Implementation
1. 创建 baozi-agent/AUTO-TRIGGER.md - 每次响应前必读
2. 更新 SKILL.md - 加入"第五部分：触发条件自动执行"
3. 流程：收到消息 → 检查清单 → 触发就写 → 处理 → 回复
### Key Principle
"宁可多记，不要漏记！不确定要不要记？→ 记！"


---

## [LRN-20260309-002] user-concern-memory-lost
**Priority**: high
**Status**: resolved
### Summary
用户担心10天后忘记今天的事情
### Details
- 张先生表达了对记忆系统的担忧
- 怕说话不能正确归档，不能自动保存
- 怕空文件里什么记忆都没有
### Context
用户在webchat中直接表达担心
### Suggested Action
- 立即将本次对话重要内容记入日记
- 确保所有触发条件真正工作

---

## [LRN-20260308203620.] correction
**Time**: 2026-03-08 20:36
你理解完全错了

## [LRN-20260308214244.] auto
**Time**: 2026-03-08 21:42
更新了working-buffer，记录了重要对话：张先生担忧记忆丢失、删除重复技能、clawhub更新技能、确认baozi-agent位置

## [LRN-20260308214349.] auto
**Time**: 2026-03-08 21:43
working-buffer已更新：张先生确认需要自动联动机制，担心context压缩后对话丢失

## [LRN-20260308214536.] auto
**Time**: 2026-03-08 21:45
自动联动测试成功：更新SESSION-STATE后调用smart-link.js，index.json同步更新到21:44:56

## [LRN-20260309150645.] correction
**Time**: 2026-03-09 15:06
测试：不是你说的那样
