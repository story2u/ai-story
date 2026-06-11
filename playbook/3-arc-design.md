# Playbook 3 · 设计剧情篇章（接力）

> 运行方式 B（默认）：本篇所有「开 X 窗口 / 贴 Y」一律读作「按 `playbook/0-cli-relay.md` 调度 X，Y 进同一个 prompt」。

目标：让"导演"模型把主线拆成 弧线 → 章节 → 场景。Showrunner 不设计剧情。

## 接力步骤
1. **取"故事至今"摘要**：开记忆管理员窗口，贴 `roles/memory-manager.md`，要它产出紧凑摘要——
   当前主线阶段、主要角色状态、世界状态、**开放伏笔与未决线索**（读摘要不读正文）。落到一段文本备用。
2. **导演设计**：开导演窗口，贴 `roles/plot-director.md` + 上一步摘要 + 本次输入（arc id / 目标字数 / 主线阶段），要它产出：
   - `story/arcs/<arc>.md`：弧线大纲、核心冲突、起承转合、要消耗/埋设的伏笔、冲突图
   - `story/chapters/<ch>.md`（多个）：每章大纲、场景清单、本章钩子、目标字数
   - `story/scenes/<sc>.md`（至少首批可演的）：scene brief，**每个出场角色须标 `knowledge`**（参考 `templates/scene-brief.md`）
3. **落盘**：把各文件存到 `story/` 对应路径。
4. **世界校验（按需）**：若导演返回 `WORLD_CHANGE_REQUESTS`，开架构师窗口裁决；`reject` 的部分让导演改方案，
   **不得带未裁决的世界变更进入演绎**。
5. **提交**：`git add story/ && git commit -m "feat(plot): 设计 <arc> 篇章"`。

## 闸门
导演 `ok` 且无未裁决世界变更 → 可进入 `playbook/4-scene-run.md`。
