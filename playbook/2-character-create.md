# Playbook 2 · 创建角色（接力）

> 运行方式 B（默认）：本篇所有「开 X 窗口 / 贴 Y」一律读作「按 `playbook/0-cli-relay.md` 调度 X，Y 进同一个 prompt」。

目标：产出 `characters/<id>.md`。由**导演**定戏剧内核、**架构师**校验世界设定，Showrunner 组装落盘。
**角色演员永不参与自己档案的创建**（防自我设计上帝视角）。

## 你需要先备好
定位 / 欲望 / 恐惧 / 外在目标 / 内在创伤 / 说话方式 / 成长弧线。

## 接力步骤
1. **导演起草戏剧内核**：开导演窗口（`cast.md`），贴 `roles/plot-director.md` + 输入，要它产出该角色的
   role、want/fear/wound/need/flaw、底线、voice、与现有角色的潜在关系/冲突、成长弧线。
2. **架构师校验世界绑定**：开架构师窗口，贴 `roles/world-architect.md`，把上一步结果 + 你的世界设定给它，
   要它校验/填充：初始境界（须合 `world/power-system.md`）、势力（`world/factions.md`）、出身地（`world/geography.md`）、
   血脉/功法是否合规。不合规它会驳回——**不得写入未过审的世界绑定字段**。
3. **你组装落盘**：按 `templates/character.md` 把两步结果合成 `characters/<id>.md`（id 用稳定 slug）。
   **必须填 `认知边界`**（开局知道什么 / 绝不知道什么 / 误以为什么）与 `演绎约束`。
4. **播种记忆**：开记忆管理员窗口，贴 `roles/memory-manager.md`，要它在
   `memory/character-state.md` 与 `memory/relationships.md` 写入该角色初始条目（位置/境界/情绪/关系边），你落盘。
5. **提交**：`git add characters/ memory/ && git commit -m "feat(char): 新增 <id>"`。

## 闸门
架构师对世界绑定字段 `approve` 且"认知边界"非空 → 完成。`reject`（越级/势力不存在）→ 交回作者调整。

> 提示：主角、女主、反派、关键配角各跑一遍。配角放 `characters/supporting/`。
