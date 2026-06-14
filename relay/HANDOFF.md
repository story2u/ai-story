# 接力板 · Codex 主控 / DeepSeek 主创

> **本板是 Showrunner 独占维护的唯一进度看板。**
> 当前作者指令(2026-06-13): Claude 额度用完，先冻结 Claude；由 Codex 当 Showrunner 主控，DeepSeek 当主创；
> Kiro / Antigravity / Cursor Agent / Ollama 尽量参与共创。CLAUDE 保留主创角色但暂不启用。
> 作者更新(2026-06-13):Codex CLI 固定使用 `/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex`;
> Antigravity CLI 为 `agy`;Kiro CLI 为 `kiro-cli`;Cursor Agent CLI 为 `agent`;Gemini 已卸载不再使用;Ollama 改用 `minimax-m3:cloud`。
> NVIDIA API 已接入为 DeepSeek 备用通道:`deepseek-ai/deepseek-v4-flash`。

## 当前通道实测

- Codex: `/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex` 可用，`codex exec` 冒烟成功(约 10.3s)；Homebrew `/opt/homebrew/bin/codex` 当前缺 vendor binary，不用。
- DeepSeek: `opencode` 可用，冒烟输出 `OK-deepseek`；当前作为主创/主要 stand-in 通道。
- NVIDIA API: `deepseek-ai/deepseek-v4-flash` 可用；`NVIDIA_API_KEY` 在 `.zshrc`,需 `zsh -ic` 读取；high thinking 冒烟成功但约 60s,仅作备用/高推理通道。
- Antigravity: `agy -p` 可用；`agy --model "GPT-OSS 120B (Medium)" -p` 冒烟成功(约 7.2s)。Gemini 已卸载,后续不再使用。
- Kiro: `kiro-cli chat --no-interactive` 可用，冒烟成功(约 7.0s)；`kiro` 编辑器入口不作为接力命令。
- Cursor Agent: `/Users/bruce/.local/bin/agent` 可用；`agent -p --mode=ask --trust` 冒烟成功，输出 `OK-cursor-agent`；用于非交互只读评审/发布自检，禁止 resume/continue 引入会话态。
- Ollama: `kimi-k2.6:cloud` 实测约 6.1s 返回 `403 Forbidden: this model requires a subscription`，弃用；`ollama run --think=false --hidethinking minimax-m3:cloud` 冒烟成功，输出干净，约 2.45s，可用于记忆/结构化任务。
- Claude: 保留在 cast 里，但当前冻结，不调度。

## 当前棒位

| 项 | 值 |
|---|---|
| 章节 | ch-0001《至贱命格》(黄金五章版) |
| 当前节点 | **ch-0001 complete / next: ch-0002 P1 认知包** |
| 前置状态 | ch-0001 正文按外部审查意见重写至 prose r4；连续性 pass(r4)；总编 pass(r4)；memory patch verified；发布前自检 pass(r5)；`memory/working/ch-0001.md` 已删除 |
| 下一棒角色 | 记忆管理员（Ollama/MiniMax M3；若再卡顿则 Kiro 备用） |
| 下一 run-id | `relay/ch-0002/sc-0002-01-packs.r1/` |
| 目标产物 | 为 ch-0002 首场编私有认知包；必须基于正式 `memory/`，不要读取已删除的 ch-0001 工作态 |

## 下一步

1. 提交并推送 ch-0001 完成态。
2. 下一章从 `story/chapters/ch-0002.md` 与 `story/scenes/sc-0002-01.md` 进入 P1 认知包。
3. ch-0002 编包输入使用正式 `memory/*.md`；不得再引用 `memory/working/ch-0001.md`。

## ch-0001 节点图

| # | 节点 | 角色@模型 | run-id | 状态 |
|---|---|---|---|---|
| D2 | 黄金前五章重设计 | plot-director@gpt | `arc-01-golden5-redesign.r1` | ✅ done，作者确认 |
| P1 | sc-0001-01 认知包 | memory-manager@claude(兼任) | `sc-0001-01-packs.r2` | ✅ done |
| B1 | sc-0001-01 演绎 | 沈砚@gpt / 柯九@gemini(历史)+deepseek stand-in | `sc-0001-01-b*` | ✅ done，6 beats；Gemini 为历史通道,后续不用 |
| L0 | b1-b4 拍抽检 | editor-spotcheck@deepseek | `sc-0001-01-spotcheck-b01-b04.r1` | ✅ pass |
| C1 | sc-0001-01 场景验收 | continuity-checker@gpt | `sc-0001-01-check.r1` | ✅ pass |
| W1 | sc-0001-01 工作态 | memory-manager@ollama(历史) | `sc-0001-01-working-memory.r1` | ✅ done；后续 Ollama 改用 minimax-m3:cloud |
| P2 | sc-0001-02 认知包 | memory-manager@ollama(历史)/deepseek stand-in | `sc-0001-02-packs.r1` | ✅ done：Ollama 超时；DeepSeek r3 accepted |
| B2 | sc-0001-02 演绎 | 沈砚@gpt/deepseek stand-in / 柯九@antigravity 或 deepseek stand-in | `sc-0001-02-b*` | ✅ done，7 beats，L0✅ |
| C2/W2 | sc-0001-02 验收+工作态 | checker+memory | `sc-0001-02-check/working` | ✅ pass(r1)，working-updated |
| P3~W3 | sc-0001-03 夜半反痕 | 多 agent | `sc-0001-03-*` | ✅ pass(r1)，working-updated→正式记忆 |
| Z1 | 正文生成 | prose-writer@deepseek | `ch-0001-prose.r1/r2/r3/r4` | ✅ done，r4 accepted（DeepSeek Pro 重写） |
| Z2~Z5 | 连续性/终审/记忆/发布前自检 | Kiro/Cursor/Kiro/Cursor | `ch-0001-*` | ✅ continuity pass(r4)，editorial pass(r4)，memory verified，pre-publish pass(r5) |

## 账本镜像

```
调度: { dispatch: 65, claude: 2, codex: 13, deepseek: 15, nvidia: 1, antigravity: 4, kiro: 7, gemini: 2, cursor: 7, ollama: 16, retry: 10, 方式A: 1, 手动CLI: 52, 兼任: 1, stand_in: 4, 作废: 7 }
```

## 最近历史

- 2026-06-13 保存 Claude 遗留进度并提交推送: `8d2b9e1 chore: save claude story progress`。
- 2026-06-13 B1.4 沈砚输出已入场记；L0 抽检通过。
- 2026-06-13 B1.5 Gemini 演员调用因容量失败；DeepSeek stand-in r1 越界引用“上一回开封”作废，r2 通过并入场记。
- 2026-06-13 B1.6 世界拍按 brief 收场，命中 sc-0001-01 exit conditions。
- 2026-06-13 sc-0001-01 L1 验收通过；Ollama 生成工作态，经 Showrunner 清理控制字符与未注册 fs-0003 后落盘。
- 2026-06-13 P2 认知包完成：Ollama 超时中断；DeepSeek stand-in r1 因沈砚包泄露柯九真相作废，r2 因未授权硬事实作废，r3 经 Showrunner 格式清理后落盘。
- 2026-06-13 B2.1 沈砚首拍完成：Codex CLI 额度耗尽（提示 2026-06-14 01:56 后可再试），DeepSeek stand-in 输出七字段合格，已入场记。下一棒 B2.2。
- 2026-06-13 通道复测:作者指定 Codex CLI 为 nvm 路径,实测可用;`agy` 与 `kiro-cli chat --no-interactive` 可用;Gemini 已卸载不再使用;Ollama `kimi-k2.6:cloud` 因订阅限制不可用,改测 `minimax-m3:cloud` 成功(约 2.45s,需 `--think=false --hidethinking`)。
- 2026-06-13 B2.2 柯九@Antigravity 完成：`agy` r1 字段名加粗作废，r2 七字段合格，已入场记。下一棒 B2.3。
- 2026-06-13 NVIDIA API 接入: `deepseek-ai/deepseek-v4-flash` high thinking smoke 输出 `OK-nvidia`, reasoning 字段存在但不进入 `out.md`;简单请求耗时约 60s,仅作备用/高推理通道。
- 2026-06-13 B2.3 世界拍完成：镇差/旧契房道具把压力转为经手簿、柜钥、卷号/押记名目；乙库未开，旧砚暂未被夺但被盯住。下一棒 B2.4 沈砚。
- 2026-06-13 B2.4 沈砚@Codex 完成：回应柯九追问，以七年拓碑/跑腿经手旧契房解释熟悉来源，并给出可查但未定案的年头/名目；b01-b04 经 Kiro/GLM L0 抽检 pass。下一棒 B2.5。
- 2026-06-13 B2.5 looping engineering 完成：Kiro 给旧契房程序微裁决，DeepSeek 生成世界拍，Ollama/MiniMax L0 pass；经手簿与乙库残卷出现可查线索，但旧具来历仍不闭环、旧砚暂记待验。下一棒 B2.6 柯九。
- 2026-06-13 B2.6 柯九@Antigravity 完成：从“旧具随工交接/来历栏空白”切入，旁敲侧击追问交接者名号；Ollama/MiniMax L0 pass。下一棒 B2.7 世界拍收束。
- 2026-06-13 B2.7/C2/W2 完成：DeepSeek 世界拍收束旧契房程序，旧砚暂归沈砚照管但三日复核、不得离身外借、不得擅离碑亭镇；Ollama L0 pass，Kiro/GLM 场景验收 pass，Ollama 工作态已并入 `memory/working/ch-0001.md`。下一棒 P3。
- 2026-06-13 sc-0001-03 完成：Ollama 编认知包；Codex/DeepSeek/Antigravity 演绎 6 拍；Ollama L0 pass；Kiro/GLM L1 pass；Ollama 工作态并入。
- 2026-06-13 ch-0001 正文完成：DeepSeek prose r1 经 Showrunner 追溯发现未登记 NPC 私名、旧砚位置链与三日复核错字，r2 修正落 `drafts/ch-0001.md`。
- 2026-06-13 ch-0001 审核完成：Kiro 连续性 r1 pass；Cursor Agent 总编 r1 因“青槐镇”地名 revise；事实源统一为“碑亭镇”后 Kiro r2 pass、Cursor Agent r2 pass。
- 2026-06-13 ch-0001 记忆落库完成：Ollama memory patch 通道卡顿中止；Kiro 备用生成 patch，经 Showrunner 审阅修正后应用，L3 回读 verified，`memory/working/ch-0001.md` 删除。
- 2026-06-13 ch-0001 发布前自检 r2 pass：补齐正文与 memory patch provenance 戳，Cursor Agent I 组复审通过，第一章可提交发布。
- 2026-06-14 作者要求核验 `docs/审查意见.md` 并用 opencode DeepSeek Pro 重写第一章：Showrunner 裁定审查意见总体合理；`opencode/deepseek-v4-pro` 因 billing 失败，改用 `deepseek/deepseek-v4-pro`。prose r3 完成节奏重写；continuity r3 打回未登记判词「五行驳杂」；落 `ch-0001-prose.r4/revision-brief.md` 后 prose r4 删除该短语，continuity r4 pass，Cursor editorial r4 pass。注意：opencode r4 通道曾直接 edit `drafts/ch-0001.md`，Showrunner 已复核并保留仅两处预期改动。
- 2026-06-14 ch-0001 pre-publish r4 pass：Cursor Agent 轻量复核通过；同步章文件/HANDOFF 至发布前 r4，并修正章纲“白天微温”漂移为夜间微温。
- 2026-06-14 ch-0001 pre-publish r5 pass：核销 r4 的账本同步与章纲漂移 WARN；剩余 WARN 为 opencode r4 直写、stand_in 批准记录、归档快照旧地名，均不阻塞发布。

created_by: showrunner@codex via codex-main · handoff-board
