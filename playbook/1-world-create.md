# Playbook 1 · 创建世界观（接力）

> 运行方式 B（默认）：本篇所有「开 X 窗口 / 贴 Y」一律读作「按 `playbook/0-cli-relay.md` 调度 X，Y 进同一个 prompt」。

目标：让"世界观架构师"模型产出整套 `world/`。Showrunner 全程不创作设定。

## 你需要先备好
小说类型 / 时代背景 / 核心冲突 / 力量体系方向 / 主角初始设定。缺关键项先问作者，**不要替作者拍板方向**。

## 接力步骤
1. **开窗口**：按 `cast.md` 找到指派给"世界观架构师"的模型，开一个干净会话。
2. **贴角色卡**：把 `roles/world-architect.md` 全文作为第一条消息（系统设定）。
3. **贴任务**：发第二条消息——
   ```
   【建世界输入】
   类型：… 时代：… 核心冲突：… 力量体系方向：… 主角初设：…
   请按你的工作流程产出这些 markdown 文件的内容，逐个文件用代码块分隔：
   world/bible.md, world/rules.md, world/power-system.md（力量体系必须可判定：每境界含能力边界/突破条件/压制关系/禁忌，建议表格）,
   world/factions.md, world/geography.md（含距离表）, world/history.md。
   最后给出 STATUS / FILES / SUMMARY / OPEN_QUESTIONS。
   ```
4. **落盘**：把它输出的每个文件内容，分别存到对应 `world/<file>.md`。
5. **拍板空白**：把 `OPEN_QUESTIONS` 原样转给作者定夺，**不要自行脑补**核心设定。
6. **提交**（若已 git init）：`git add world/ && git commit -m "feat(world): 世界观奠基"`。

## 闸门
架构师 `created` 且无阻塞性 OPEN_QUESTIONS → 完成。`rejected`（设定自相冲突）→ 把冲突点交回作者重来。

> 下一步：`playbook/2-character-create.md` 建主角。
