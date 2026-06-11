# Playbook 6 · 审核与记忆更新（接力）

> 运行方式 B（默认）：本篇所有「开 X 窗口 / 贴 Y」一律读作「按 `playbook/0-cli-relay.md` 调度 X，Y 进同一个 prompt」。

目标：守章级两道闸门，过审后落库记忆并提交。设章节 id `<ch>`；每道闸门轮次 `r<N>` 从 r1 起计。
**任一闸门不过即按循环宪法回退（`HARNESS.md §10`）：落盘 revision-brief、计轮次；
单闸≤2 轮修订、全章累计≤4 轮，耗尽→升级作者。绝不带病发布，也绝不无限重做。**

## 闸门 A：机械核对（连续性检查器 · 便宜验证在前）
开连续性检查器窗口，贴 `roles/continuity-checker.md` + 输入（`drafts/<ch>.md`、上一章草稿、本章全部场记、
`memory/character-state.md`、`memory/timeline.md`、`world/geography.md`）。除其清单 7 项外，加做**追溯抽查**：
抽正文 3–5 个情节点，对照场记与 meta 的 `beats_covered` 反向定位到具体拍——
**找不到对应拍 = 输出器越权创作**（BLOCKER）。`beats_covered` 是输出器的"声明"，这一步把声明变成"证明"。
落 `reviews/<ch>.continuity.r<N>.md`。
- `revise` → Showrunner 依报告写 revision-brief（`rb-<ch>-rN`，模板 `templates/revision-brief.md`）：
  细节连贯/呈现层问题回 `playbook/5`；事实硬伤（场记本身错）回 `playbook/4` 重演相关拍。
  修完轮次 +1 重跑本闸门——**增量复审**：先核销上轮 ISSUES，再抽查受影响接缝，不全量重审。

## 闸门 B：总编终审（判断力项）
闸门 A `pass` 后，开总编窗口，贴 `roles/editor.md` + 输入（草稿、场记、scene brief、`world/`、`characters/`、`memory/`）。
落 `reviews/<ch>.editorial.r<N>.md`。
- `revise` → 按 `RETURN_TO` 写 revision-brief 回退 perform/prose；修完重跑 **A+B（均增量）**。
  复审输入 = 上轮报告 + revision-brief + 改动摘要；总编先核销旧 BLOCKERS，并对再次出现的问题标 `REPEAT`。
- `reject` → 结构性问题，回 `playbook/3` 重设计或重演关键场景（计入全章回退轮次）。
- `needs-world-ruling` → 开架构师窗口裁决，据裁决修正后重跑。
- `pass` → 进入记忆更新。

## 预算与升级（L2 循环边界）
- 单闸门修订 ≤2 轮（至多 r3）；全章累计回退 ≤4 轮。每轮写入章文件"流水线状态"（`连续性: {r1: revise(3), r2: pass}`）。
- **预算耗尽 ≠ 放水通过。** Showrunner 整理**分歧摘要**（审稿立场+证据 vs 现稿理由）交作者裁决；拍板前本章冻结。
- 审报中 `REPEAT` 非空的条目 → 让记忆管理员记入 `memory/lessons.md`；同类第 2 次 → 必须硬化
  （流程见 `playbook/7-arc-retro.md` §B，紧急的可立即做，不必等弧线收尾）。

## 记忆更新（memory_patch · L3 循环）
1. 开记忆管理员窗口，贴 `roles/memory-manager.md`，要它依据场记 `proposed_deltas`、`memory/working/<ch>.md` 与正文，
   产出 `memory/patches/<ch>.patch.md`（参考 `templates/memory-patch.md`，先 `patch-ready` 不立即应用）。
2. **你审阅补丁摘要**（变更与正文一致？伏笔回收有无遗漏？）。有疑问让它修正（**patch 修订≤2 轮**，仍存疑→你人工逐条比对）。
3. 确认后让它**应用**补丁——逐条幂等编辑各 `memory/*.md`（稳定 id 去重）。你落盘。
4. **回读校验（L3 出口）**：让它对照 patch 逐条回读 `memory/*.md`——每条 id 存在、无重复、字段一致，报 `verified`；
   不一致 → 修正重验。verified 后**删除 `memory/working/<ch>.md`**（工作态已被正式记忆取代）。
5. 让导演把本章 `摘要` 回填到 `story/chapters/<ch>.md`（滚动摘要，供日后只读摘要）。

## 发布（git 一次性提交）
对照 `checklists/pre-publish.md` 过一遍（含 H 组"循环卫生"），然后：
```bash
git add drafts/<ch>.md memory/ reviews/<ch>.* story/chapters/<ch>.md
git commit -m "feat(<ch>): <章标题>"
```
弧线收尾时跑 `playbook/7-arc-retro.md`（债务盘点+教训硬化），完成后可 `git tag <arc>-complete`。
