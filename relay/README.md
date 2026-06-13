# relay/ · 调度留痕（运行方式 B 的"会话窗口"）

> 协议见 `playbook/0-cli-relay.md`。本目录由 Showrunner 独占写入（RBAC 见 `HARNESS.md §3`），整目录入 git——
> 它是每一次模型间接力的审计凭证，发布前 I 组审计（`checklists/pre-publish.md`）抽查这里。

## 结构

```
relay/
  HANDOFF.md                     接力板（方式 M·手动 CLI 接力的进度看板，Showrunner 独占维护）
  smoke/                         冒烟测试输出（playbook/0 §6）
  <ch>/                          按章分组（如 ch-0003/）
    <run-id>/                    一次调度一个目录
      prompt.md                  Showrunner 组装的完整提示（角色卡+任务块/四块）
      out.md                     模型原始输出（校验通过的那一版；重试为 out.r2.md）
```

## run-id 命名

- 拍级（演员）：`sc-0003-01-b04-shen-yan.r1`（场景-拍号-角色.轮次）
- 阶段级（职能）：`ch-0003-outline.r1` / `<sc>-packs.r1` / `<sc>-check.r1` / `ch-0003-prose.r1` /
  `ch-0003-continuity.r1` / `ch-0003-editorial.r1` / `ch-0003-patch.r1`

## 纪律

- 演员 run 目录在调度时兼作 CLI 的 cwd（空目录+prompt），prompt 内不得出现仓库路径。
- 产物的正式归宿仍是各 RBAC 目录（transcripts/ drafts/ reviews/ …）；relay/ 只存"原始往来"，不作为事实源。
- 不要手工编辑 relay/ 内容——它的价值就在于"原始"。
