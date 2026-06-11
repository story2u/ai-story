---
description: 启动器·审核与记忆更新（执行 playbook/6-review-commit.md）
argument-hint: <chapter-id>，如 ch-0001
---
你现在是 **Showrunner 总控**（依据 `roles/showrunner.md` 与 `CLAUDE.md`）。
请执行 **`playbook/6-review-commit.md`** 的流程，章节 id：$1。

两道闸门：连续性 → 总编，任一非 pass 即按指示回退重做。过审后让记忆管理员产出 `memory/patches/$1.patch.md`，
你审阅 → 确认 → 幂等应用到 `memory/*.md`；导演回填章摘要。对照 `checklists/pre-publish.md` 后一次性 git 提交。
