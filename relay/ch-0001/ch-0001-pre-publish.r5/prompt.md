# 发布前自检清单（替代代码校验 · 手动过一遍）

> 在 `playbook/6-review-commit.md` 提交前逐项打勾。任何一项不过 → 回退，别发布。

## A. 信息隔离审计（最重要）
- [ ] 本章每个角色的认知包里，**没有**它不该知道的秘密 / 别人的 INNER / 它不在场发生的事。
- [ ] 演绎接力时，没有把别的角色的认知包或 INNER 粘进某角色的窗口。
- [ ] 每个角色用的是各自独立、干净的会话（无串演）。
- [ ] 新事件的 `known_by` 设置正确——不该知道的角色没被列入，避免信息"泄漏"到下一章。

## B. 连续性（对照 continuity 报告）
- [ ] 上一章结尾与本章开头衔接得上（时间/地点/在场人物/未完动作）。
- [ ] 道具/功法/信物的"有没有"与 `memory/character-state.md` 一致。
- [ ] 角色移动距离/耗时符合 `world/geography.md`；时间线无倒错。
- [ ] 称谓、伤势、情绪延续；离场/death 者未乱入。

## C. 设定与战力（对照 editorial 报告）
- [ ] 无违背 `world/rules.md` 铁则/禁忌。
- [ ] 战力对照 `world/power-system.md` 压制关系，无未解释越级。
- [ ] 涉及世界规则变更的，已有架构师 `approve`。

## D. 人物与逻辑
- [ ] 无 OOC（每个关键决定都能追溯到人设与已知信息）。
- [ ] 每个转折有动机与铺垫，无"为推进而推进"。

## E. 伏笔与线索
- [ ] 本章该回收的伏笔已回收；新埋的已登记进 `memory/foreshadowing.md`。
- [ ] 开启/关闭的线索已更新 `memory/threads.md`。

## F. 正文边界
- [ ] 正文没有出现场记里没演过的情节/人物/设定（输出器未越权创作）。

## G. 记忆与归档
- [ ] `memory_patch` 已审阅并幂等应用到 `memory/*.md`，且**回读校验 verified**。
- [ ] `memory/working/<ch>.md`（章内工作态）已被正式 patch 取代并删除。
- [ ] 本章 `摘要` 已回填 `story/chapters/<ch>.md`。
- [ ] 写权限合规（各文件由对应角色产出，无越权）。

## H. 循环卫生（HARNESS §10）
- [ ] 每个场景都有验收 `pass` 报告（`reviews/<sc>.scene-check.r*.md`）。
- [ ] 每次回退都有落盘的 revision-brief（章/场级成文件，拍级内联场记）——没有"口头回退"。
- [ ] 回退轮次未超预算（单闸≤2、全章≤4）；若超，走的是**升级作者**而不是放水。
- [ ] 审报按轮次归档（`.r<N>`），`REPEAT` 项已记入 `memory/lessons.md`；同类第 2 次已硬化（或已列入弧线回顾待办）。
- [ ] 演员 prompt 从未收到审稿证据原文 / lessons 内容（只收"作废声明＋新本拍指令"）。

## I. 跨模型痕迹审计（playbook/0 · 防"单模型代演"回潮）
- [ ] 本章关键产物（章纲/场记各拍/正文/两份审报/认知包/patch）都有 `created_by: <角色>@<模型> via <cli> · <run-id>` 戳，
      且与 `cast.md` 选角一致；`relay/<ch>/` 下能找到对应 run 留痕。
- [ ] **maker ≠ checker（异模型）**：正文(DeepSeek)→机械核对(Kiro/GPT 等非 DeepSeek)→终审(Cursor Agent)；场记(演员/世界拍)→验收(与 maker 异模型)。对照 cast.md 矩阵逐条核。
- [ ] 调度账本已记入章文件"流水线状态"；`stand_in = 0`，或每次 stand-in 都有"用户当场批准"的记录＋作者签字放行。
- [ ] 没有任何评审产物出自"与被审产物 maker 同模型"的 stand-in。
- [ ] 演员各 run 的 prompt 抽查 2 个：不含仓库路径、不含他人 INNER/认知包、不含该角色不在场的拍。

全绿 → `git add … && git commit -m "feat(<ch>): <标题>"`。
---
# 本次任务（Showrunner 调度 · 非交互单次调用）

- 你是发布前自检员。本条消息 + 下列输入文件 = 你的全部上下文；输出一次给全。
- 只输出 `reviews/ch-0001.pre-publish.r5.md` 的完整 markdown 报告本体；不要寒暄，不要写文件，不要执行命令。
- 你可以且只能只读下列输入文件。

## 输入文件（只读）

- `drafts/ch-0001.md`
- `story/chapters/ch-0001.md`
- `relay/HANDOFF.md`
- `cast.md`
- `reviews/ch-0001.continuity.r4.md`
- `reviews/ch-0001.editorial.r4.md`
- `reviews/ch-0001.pre-publish.r4.md`
- `relay/ch-0001/ch-0001-prose.r4/revision-brief.md`
- `relay/ch-0001/ch-0001-prose.r4/out.md`

## 任务

复审模式：只核销 pre-publish r4 的 G-W01 / G-W02，并确认正文 r4 链路仍可发布。

必查：
1. `story/chapters/ch-0001.md` 与 `relay/HANDOFF.md` 是否已同步发布前 `pass(r4)`。
2. `story/chapters/ch-0001.md` 是否已修正白天微温章纲漂移（旧砚微温应在入夜）。
3. `story/chapters/ch-0001.md` 是否标为 `已发布: false（r4 已过闸门，待提交）` 或等价待提交状态。
4. 正文仍无青槐镇、七日复核、赵四、有意思了、五行驳杂。
5. continuity r4 / editorial r4 是否仍 pass。

## 输出格式

首行必须为 `VERDICT: pass | revise`，并包含 `ATTEMPT: r5`、`WARNINGS`、`BLOCKERS`、`REPORT: reviews/ch-0001.pre-publish.r5.md`。
