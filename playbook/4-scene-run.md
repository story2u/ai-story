# Playbook 4 · 场景演绎（接力 · 系统最核心动作）

> 运行方式 B（默认）：本篇所有「开 X 窗口 / 贴 Y」一律读作「按 `playbook/0-cli-relay.md` 调度 X，Y 进同一个 prompt」。
> 演员调度必须用演员模板（playbook/0 §3b）：cwd 锁空 run 目录、prompt 不含仓库路径、禁读文件禁用工具。

目标：把一个 scene brief 演成 `transcripts/<sc>.md`。
你是 Showrunner，本场唯一上帝视角。**所有角色互动由你居中接力**，且**绝不把角色不该知道的信息递给它**。

设场景 id 为 `<sc>`，读 `story/scenes/<sc>.md` 作为 brief。

## 0. 读 brief
取 `goal / location / participants（含各自 knowledge）/ conflict / director_constraints / exit_conditions / beat_budget`。

## 1. 编私有认知包（信息隔离）
开记忆管理员窗口，贴 `roles/memory-manager.md` + 本 brief，要它为每个 participant 产出
`context_packs/<sc>.<char>.md`，落盘。记下它给的"信息不对称点"——这是你制造张力的弹药。
**编包输入 = `memory/`（章前快照）+ `memory/working/<ch>.md`（本章已演场景的工作态）**——
这保证 sc-02 的角色"记得"sc-01 的后果（见其角色卡职责一）。本章首场则无工作态，仅快照。

## 2. 初始化场记
新建 `transcripts/<sc>.md`，写头部：场景目标、地点、出场人物、初始情境（公开信息）。

## 3. 回合循环（每一拍 = 一次调度）
重复，直到命中 `exit_conditions` 或耗尽 `beat_budget`：

1. **定序**：首拍按 brief 的 opening 顺序；之后按"谁被点名/被针对/情绪驱动"决定下一个谁动。
   拿不准节奏/该不该转折时，开导演窗口要一条**只含目标与限制、不含台词**的本拍指令。
   **环境/世界事件**（异象、天气突变、第三方闯入）也走导演本拍指令注入——"世界拍"；
   **不要**把"今晚将发生什么"预写进认知包（盲区段只许写"你不知道 X 存在"，不许写事件脚本）。
2. **调度该角色演本拍**（`cast.md` 指派的模型）。方式 B 每拍 = 一次**无状态**调用，prompt 必须装齐、且**仅**装：
   - **角色卡**：`roles/character-actor.md` 全文（无会话记忆，每拍都要带）
   - **YOU ARE**：`characters/<id>.md` 的人设要点
   - **你的私有认知包**：`context_packs/<sc>.<id>.md` 全文
   - **公开场记（仅该角色亲历的拍，且只含 SPEAK/ACT）**——见下方"可见性过滤"
   - **导演本拍指令**（回应谁/什么情境，限制）
   （方式 A 的固定会话里，角色卡与 YOU ARE 首拍贴过可省；方式 B 无可省，每拍全量重发——
   角色的连续性来自认知包与场记，不来自会话。）
3. **取回 7 字段**（SPEAK/ACT/INNER/BASIS/STATE_DELTA/KNOWLEDGE_GAINED/FLAG）。
   - 若 `FLAG` 非空（拒演 OOC / 被要求用未知信息）：**角色是对的**。别硬掰——开导演窗口改本拍意图，或顺势把"拒绝"写成转折。
4. **写入一拍**到 `transcripts/<sc>.md`，带可见性标签：
   ```
   ## Beat <n> · <char-id> · visibility=public | aside(听见的人) | solo
   SPEAK: …
   ACT: …
   INNER(private): …
   BASIS: …
   STATE_DELTA(proposed): …
   KNOWLEDGE_GAINED: …
   ```
5. **抽检（L0 验证）**：每 3–5 拍，或出现疑似越界/战力异常时，开总编窗口贴 `roles/editor.md` 做轻量点检（OOC/逻辑/战力）。
   verdict 记入场记：`SPOT_CHECK(beat n–m): pass | flag(beat k: 理由)`。
   被 flag → **作废该拍重演**（单拍重演≤2，`HARNESS.md §10` L0）：场记中该拍标 `[作废·r1]` 保留原文，
   紧随写**内联修订块**（字段同 `templates/revision-brief.md`：证据/为何/改法方向/新约束），再据它组装新的本拍指令。
   **演员窗口只收"第 n 拍作废"声明 + 新本拍指令**，绝不收审稿证据原文。两轮仍 flag → 升级导演改本拍意图。

### 可见性过滤（防上帝视角的执行细节）
给角色 B 拼"公开场记"时，**只**纳入：`visibility=public` 拍的 SPEAK+ACT；`aside(...)` 中**包含 B** 的拍。
排除：**所有人的 INNER**、B 不在场的 solo/aside 拍、B 退场后的内容。**任何角色都拿不到别人的 INNER。**

## 4. 收尾
在 `transcripts/<sc>.md` 末尾追加：
```
## SCENE RESULT
outcome: 本场结果（谁赢/关系如何变/得失什么）
emotional_beats: [关键情绪转折]
proposed_deltas: [汇总各拍 STATE_DELTA，留给记忆管理员落库用]
foreshadow_touched: [本场埋设/触及的伏笔 id]
```
**本阶段不更新 `memory/`**（正式落库在章节过审之后，见 `playbook/6-review-commit.md`；
但验收 pass 后，`proposed_deltas` 要并入**章内工作态**，见下一步）。

## 5. 场景验收（L1 闸门 · 便宜验证在前）

收尾后、开演下一场或进入正文**之前**，开连续性检查器窗口（`cast.md`），贴 `roles/continuity-checker.md` +
本场 brief + 完整场记 + 本场全部认知包，要它按其角色卡"任务二·场景验收"做**四项机械核对**：

1. **导演限制**逐条守住？（如"柯九不得暴露修为"——在场记里逐拍找反例）
2. **收场合规**：命中某条 exit_condition，或 beat_budget 耗尽且收得不突兀？
3. **伏笔落地**：brief 声明的 plant/payoff 在场记中有真实的拍支撑？
4. **隔离审计**：可见性标签正确；SCENE RESULT 的"隔离自检"自报属实——无人收到过他人 INNER / 不在场拍 / `must_not_know` 内容。

verdict 落 `reviews/<sc>.scene-check.r<N>.md`。
- `redo` → 写场级 revision-brief（`rb-<sc>-rN`），点名重演具体拍（回步骤 3）；**验收重演≤2 轮**，仍不过 → 升级导演改 brief。
- `pass` → 章文件"流水线状态"记 `sc-xx: done·验收pass(rN)`；并让记忆管理员把 SCENE RESULT 的
  `proposed_deltas` 并入 `memory/working/<ch>.md`（章内工作态——后续场景编包的依据，过审后被正式 patch 取代）。

> 下一步：本章场景全部演完且验收 pass → `playbook/5-prose-generate.md`。
