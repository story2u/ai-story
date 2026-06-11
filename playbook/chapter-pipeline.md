# Playbook · 整章流水线（把 1→6 串起来）

> 运行方式 B（默认）：所有角色一律按 `playbook/0-cli-relay.md` 调度对应 CLI，主会话不代演。
> 开章前先跑冒烟测试（playbook/0 §6），三通道全通再开演。

按状态机生产一整章。设章节 id `<ch>`。

```
建大纲 → 编认知包 → 逐场景演绎+验收 → 生成正文 → 机械核对 → 终审 → 记忆补丁+校验 → 发布
 P3        P4(步1)      P4(步3-5)        P5        P6-A       P6-B    P6              git
                          ▲                                            │
                          └────── revision-brief 回退（计轮次）◀───────┘
                  预算：场景验收重演≤2 ｜ 单闸修订≤2 ｜ 全章累计≤4 → 耗尽升级作者（HARNESS §10）
```

## 断点续跑（上下文不失控的关键）
每完成一个阶段，把进度写进 `story/chapters/<ch>.md` 的"流水线状态"段。**带循环账本（loop ledger）的 schema**：

```
- 演绎: { sc-0001-01: done·验收pass(r1), sc-0001-02: redo(r1→重演beat4,5) }
- 正文: done
- 连续性: { r1: revise(3 issues, rb-ch-0001-r1), r2: pass }
- 终审: { r1: pending }
- 记忆: patch r1 applied·verified ｜ 工作态: memory/working/<ch>.md 已清
- 调度: { dispatch: 23, claude: 6, codex: 9, deepseek: 8, retry: 1, 方式A: 0, stand_in: 0 }
- 回退累计: 1/4
- 已发布: false
```

总控对话被压缩/重开后，先读这段从断点续跑——轮次与最近 verdict 都在，能直接续在"循环中段"
（知道这是第几轮、上轮为什么挂、对应哪份 revision-brief），**不要重头再来、不要把已完成正文读回上下文**。

## 步骤
1. **大纲检查**：读 `story/chapters/<ch>.md`。无场景清单 → 先跑 `playbook/3-arc-design.md`。
2. **逐场景演绎+验收**：对场景清单里每个未完成的 `<sc>`，执行 `playbook/4-scene-run.md` 全流程
   （编认知包→回合接力→出 transcript→**场景验收**→工作态并入 `memory/working/<ch>.md`）。
   每完成一场更新"流水线状态"，**总控里只留该场一句话 outcome**。
3. **正文**：执行 `playbook/5-prose-generate.md`。`insufficient` → 回到对应场景补演。
4. **审核 + 记忆 + 提交**：执行 `playbook/6-review-commit.md`。任一闸门回退：写 revision-brief、
   计轮次、按指示修复后回到对应阶段；**预算耗尽即升级作者，不放水**。
5. **完成**：流水线状态 = published。

## 守则提醒
你只调度不创作（主会话不代演任何角色）；传路径不传正文；闸门不过不前进；回退必有落盘的 revision-brief；
预算耗尽升级而非放水；每章必落库记忆（patch 应用后回读校验）；
所有角色经 `playbook/0-cli-relay.md` 调度，通道故障按降级阶梯（重试→方式A粘贴→批准的 stand-in→暂停），调度账本随阶段更新。
