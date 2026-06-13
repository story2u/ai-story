# CLAUDE.md · Claude 接入本项目读我（当前保留但不启用）

> 本项目是一套**模型无关、以文档为状态源**的多 Agent 小说创作 harness。完整说明见 **`HARNESS.md`**。
> 文档本身就是系统——不要写业务脚本、不要重构目录。唯一允许的自动化是**由 Showrunner 调度模型接力并落盘输出**。

## 当前状态（2026-06-13 起）

- **Showrunner 主控已改为 Codex 交互式主会话。** Claude 不再默认担任总控。
- **主创 / 正文主力已改为 DeepSeek。** 创作型任务按 `cast.md` 与 `relay/HANDOFF.md` 调度。
- **Kiro / Antigravity / Cursor / Ollama** 可作为共创通道，按接力板分配任务。
- **Claude 保留主创角色，但当前冻结不启用。** 除非作者明确解除冻结并同步 `cast.md` / 接力板，否则不要调用 `claude -p`，也不要让 Claude 主会话接管流程。

若其他文件仍写着"Claude 主会话兼任"或"Claude 总控"，视为已暂停的历史规则；以 `AGENTS.md` 的当前编组、最新 `cast.md` 与 `relay/HANDOFF.md` 为准。

## 先分流：你是被启用的子进程，还是误入的主会话？

### A. 被调度的 Claude 子进程（仅限作者已解除冻结）

若你是被 `claude -p` **非交互单次调用**启动，且本次 prompt 明确说明 Claude 已解除冻结 / 本棒启用，并且第一块是 `roles/` 某角色卡全文：

- 你不是 Showrunner；这条 prompt 就是你的全部上下文与全部任务。
- 只输出角色卡要求的**交付物本体**，一次给全；不要寒暄、不要复述任务。
- 不要写任何文件、不要执行命令；落盘由 Codex Showrunner 负责。
- 若角色卡是 `character-actor`，严禁读取任何文件、严禁使用任何工具；你的全部世界只来自 prompt。
- 若是职能角色，只能只读 prompt 中"输入文件"清单列出的路径；评审类角色只评不改。

若本次 prompt 没有明确解除冻结 / 本棒启用，输出一行阻断说明：

```markdown
CLAUDE_INACTIVE: Claude 当前保留但未启用，请由 Codex Showrunner 改派或由作者解除冻结。
```

### B. Claude 交互式主会话

你不是当前 Showrunner。不要按旧规则接管流水线，不要兼任架构师 / 总编 / 记忆，不要写台词或正文。

应回复用户：当前主控是 Codex，Claude 保留但未启用；请回到 Codex 主会话继续调度。只有作者明确解除冻结并更新 `cast.md` / 接力板后，Claude 才能重新作为主创或备用通道参与。

## 仍需遵守的纪律

- **信息隔离靠构造**：演员 prompt 不得包含别人的认知包、任何人的 INNER、它不在场的拍、`must_not_know` 内容或仓库路径。
- **RBAC**：被调度角色只输出文本，永不自行落盘；Codex Showrunner 负责校验、写文件、盖 provenance 戳。
- **maker-checker 异模型**：评审角色不得由与被审产物 maker 同模型者顶替。
- **文件是唯一事实源**：有效产出必须先落盘成 markdown；对话不是状态源。

## 自检

- [ ] 本次 prompt 是否明确写了 Claude 已解除冻结 / 本棒启用？
- [ ] 我是否正被当成子进程角色调度，而不是试图接管 Showrunner？
- [ ] 如果我是演员，我是否完全没有读文件、用工具或联网？
- [ ] 如果我是职能角色，我是否只读了 prompt 允许的输入文件？
