# Playbook 7 · 弧线回顾（L4 系统循环 · 让循环改进循环）

> 运行方式 B（默认）：本篇所有「开 X 窗口 / 贴 Y」一律读作「按 `playbook/0-cli-relay.md` 调度 X，Y 进同一个 prompt」。

目标：每条弧线收尾时跑一次——盘清叙事债务、把审稿教训硬化为系统规则。设弧线 id `<arc>`。
这是唯一一个**改进 harness 本身**的工作流：前六个 playbook 生产小说，这一个生产"更好的生产方式"。

## A. 叙事债务盘点（伏笔与线索不允许无限挂账）
1. 开记忆管理员窗口，贴 `roles/memory-manager.md`，要它产出**债务报告**：
   - `memory/foreshadowing.md` 全部 `open` 伏笔：id / 埋于 / **age（已历章数）** / 原拟回收点；
   - `memory/threads.md` 全部 `open` 线索：同上。
2. 开导演窗口，贴 `roles/plot-director.md` + 债务报告，要它**逐条裁决**（不许跳过）：
   - `如期`——拟回收点仍有效，注明落在哪个 arc/章；
   - `延期`——给出**新的**拟回收点（不允许"以后再说"）；
   - `abandoned`——注销，写明理由（读者已无感知 / 与新方向冲突）。
3. 记忆管理员把裁决落库（更新 `foreshadowing.md` / `threads.md` 状态字段），Showrunner 落盘。

## B. 教训提炼与硬化（lessons 飞轮）
1. 记忆管理员汇总本弧 `memory/lessons.md` 中所有 `open` 条目与本弧全部审报的 `REPEAT` 项。
2. 对**出现 ≥2 次的同类教训，必须硬化**（`HARNESS.md §10` 铁律 4），由 Showrunner 按 RBAC 转交对应所有者落笔：
   - 文风/呈现类 → `drafts/STYLE.md` 新规则（输出器落笔）；
   - 导演限制类 → `templates/scene-brief.md` 的"导演限制"加示例条目（导演落笔）；
   - 机械核对类 → `checklists/pre-publish.md` 或检查器清单加一项；
   - 人设类 → `characters/<id>.md` 的 `cognition_rules` 补充（走 `/character-create` 联署流程）。
3. 记忆管理员把已硬化条目标记 `hardened→<去处>`。**硬化后该类问题再犯 = 系统性事故，直接升级作者。**
4. ⚠️ 隔离纪律：lessons 原文与"系统在抓什么"的讨论，**永不进演员窗口**；演员只通过更好的导演限制间接受益。

## C. 弧线收尾归档
1. 导演把弧线 `摘要` 回填 `story/arcs/<arc>.md`（三级滚动摘要的顶层）。
2. 核对本弧各章"流水线状态"均 `published`、回退轮次无超预算未升级的记录。
3. 提交并打标：
```bash
git add memory/ story/arcs/<arc>.md drafts/STYLE.md templates/ checklists/
git commit -m "chore(<arc>): 弧线回顾——债务盘点+教训硬化"
git tag <arc>-complete
```

## 闸门（L4 出口）
债务逐条有裁决（无"挂着再说"）＋ ≥2 次教训全部硬化 → 完成，可设计下一弧线（回 `playbook/3-arc-design.md`）。
