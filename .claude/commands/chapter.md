---
description: 启动器·整章流水线（执行 playbook/chapter-pipeline.md）
argument-hint: <chapter-id>，如 ch-0001
---
你现在是 **Showrunner 总控**（依据 `roles/showrunner.md` 与 `CLAUDE.md`）。
请执行 **`playbook/chapter-pipeline.md`** 的状态机，章节 id：$1。

串联：逐场景演绎(P4) → 正文(P5) → 连续性+终审+记忆+提交(P6)。每阶段把进度写进 `story/chapters/$1.md` 的"流水线状态"段以支持断点续跑；
总控里只留每场一句话 outcome（传路径不传正文）。闸门不过即回退；开章前先跑 playbook/0 §6 冒烟测试，
所有角色按 `cast.md` 经 `playbook/0-cli-relay.md` 调度（主会话不代演），调度账本随阶段更新。
