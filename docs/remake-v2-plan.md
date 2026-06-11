# ch-0001 / ch-0002 v2 重制计划（多模型轮动版）

> 决策（作者，2026-06-12）：v1 两章为单模型产物（全部角色被 Showrunner=Claude stand-in 代演，
> maker-checker 失效），**两章全部按运行方式 B（`playbook/0-cli-relay.md`）重制**。
> 章纲/场景 brief/世界观/角色档案等**设计资产保留**，表演与正文全部重来。

## 已完成的准备（本计划落盘的同一提交）

- **归档**：v1 产物移入 `drafts/v1/`、`transcripts/v1/`、`reviews/v1/`、`context_packs/v1/`、`memory/patches/v1/`。
  v1 正文可读可对照，但不再是流水线状态的一部分。
- **记忆回滚**：`memory/` 六个状态文件（events/timeline/character-state/relationships/foreshadowing/threads）
  回滚至 ch-0001 演绎前基线（commit `4809850`）。**`memory/lessons.md` 保留**（3 条流程教训与其硬化产物
  ——characters/ke-jiu v2 认知边界、templates/context-pack 警示句、playbook/4 世界拍规则——是系统资产，不随剧情回滚）。
- **流水线重置**：`story/chapters/ch-0001.md`、`ch-0002.md` 状态清零，调度账本归零。

## 重制步骤（在 Mac 上以 Claude Code 为 Showrunner 执行）

1. **冒烟测试**（playbook/0 §6）：三通道各发一条自报家门，全通才开工。
2. **导演复核（GPT@codex）**：调度导演读 `story/arcs/arc-01.md`、两章章纲、5 个场景 brief（v1 stand-in 起草），
   逐份给 `认可 / 修订`（修订直接给新稿，Showrunner 落盘并盖戳）。这一步让设计资产真正归属导演。
3. **`/chapter ch-0001`**：按新协议跑全章——
   - 认知包：memory-manager@claude（`claude -p`）；柯九档案用 v2 认知边界（iso-001 硬化成果）。
   - 演绎：沈砚@codex、柯九@claude（`claude -p`）逐拍轮动；每拍一个 relay run。
   - 场景验收:continuity-checker@codex；正文:prose-writer@deepseek（opencode）;机械核对:@codex;终审:editor@claude。
   - 字数目标沿用 v1 终审裁定的 2400（ed-001 教训,已注记在章纲 front-matter）。
4. **对照复盘（轻量）**：ch-0001 v2 发布后，把 v2 与 `drafts/v1/ch-0001.md` 并排读一遍，
   重点看:声音差异是否出现(沈砚/柯九异模型)、审报是否抓到 v1 抓不到的问题。值得记的写进 lessons。
5. **`/chapter ch-0002`**：同上(苏决@deepseek 首次登场,三家演员齐轮动)。
6. 两章发布后,若对 v1→v2 提升满意,删除本计划的"待办"性质,转为存档记录;继续 ch-0003。

## 验收标准（这次重制要证明的事）

- [ ] 全程 0 次未批准 stand-in；调度账本三家计数均 >0。
- [ ] 每个产物 `created_by` 戳与 `cast.md` 一致;I 组审计全绿。
- [ ] 正文(DeepSeek)→机械核对(GPT)→终审(Claude) 全链异模型,审报至少一条实质 issue(异模型应能看见同模型盲区)。
- [ ] 三个演员的台词风格肉眼可辨(声音差异是多模型的核心收益)。

created_by: showrunner-prep@claude via cowork · 2026-06-12
