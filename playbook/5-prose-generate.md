# Playbook 5 · 生成正文（接力）

> 运行方式 B（默认）：本篇所有「开 X 窗口 / 贴 Y」一律读作「按 `playbook/0-cli-relay.md` 调度 X，Y 进同一个 prompt」。

目标：让"小说输出器"模型把某章全部场记写成正文。它**只呈现、不创作**。设章节 id 为 `<ch>`。

## 接力步骤
1. 读 `story/chapters/<ch>.md`，取其场景清单与 `style`、目标字数、钩子意图。
2. 确认每个场景的 `transcripts/<sc>.md` 都已存在（缺则先回 `playbook/4-scene-run.md`）。
3. **开输出器窗口**（`cast.md`），贴 `roles/prose-writer.md`，再贴：本章全部 transcript 内容、章节大纲、
   相关角色的 voice（来自 `characters/*.md`）、风格（`drafts/STYLE.md` 或章纲 `style`）。要求：
   - 正文每一情节都能追溯到场记的拍；**不得新增情节、不得改角色意图、不得引入新设定**。
   - 产出 `drafts/<ch>.md`：章标题 + 正文 + 章尾钩子 + meta（next_hook / word_count / beats_covered）。
4. **落盘**到 `drafts/<ch>.md`。
5. 若返回 `insufficient`（场记断层）→ **不要让它脑补**，把 `GAPS` 交回导演补演（回 `playbook/4`）。

## 注意
正文先**不提交**，等连续性 + 总编过审后随记忆补丁一并提交（`playbook/6-review-commit.md`）。
