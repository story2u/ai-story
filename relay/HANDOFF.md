# 接力板 · Codex 主控 / DeepSeek 主创

> **本板是 Showrunner 独占维护的唯一进度看板。**
> 当前作者指令(2026-06-13): Claude 额度用完，先冻结 Claude；由 Codex 当 Showrunner 主控，DeepSeek 当主创；
> Kiro / Antigravity / Cursor / Ollama 尽量参与共创。CLAUDE 保留主创角色但暂不启用。
> 作者更新(2026-06-13):Codex CLI 固定使用 `/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex`;
> Antigravity CLI 为 `agy`;Kiro CLI 为 `kiro-cli`;Gemini 已卸载不再使用;Ollama 改用 `minimax-m3:cloud`。

## 当前通道实测

- Codex: `/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex` 可用，`codex exec` 冒烟成功(约 10.3s)；Homebrew `/opt/homebrew/bin/codex` 当前缺 vendor binary，不用。
- DeepSeek: `opencode` 可用，冒烟输出 `OK-deepseek`；当前作为主创/主要 stand-in 通道。
- Antigravity: `agy -p` 可用；`agy --model "GPT-OSS 120B (Medium)" -p` 冒烟成功(约 7.2s)。Gemini 已卸载,后续不再使用。
- Kiro: `kiro-cli chat --no-interactive` 可用，冒烟成功(约 7.0s)；`kiro` 编辑器入口不作为接力命令。
- Cursor: Cursor.app 存在；`cursor-agent` / `cursor` 当前不在 PATH，暂不能命令棒调用。
- Ollama: `kimi-k2.6:cloud` 实测约 6.1s 返回 `403 Forbidden: this model requires a subscription`，弃用；`ollama run --think=false --hidethinking minimax-m3:cloud` 冒烟成功，输出干净，约 2.45s，可用于记忆/结构化任务。
- Claude: 保留在 cast 里，但当前冻结，不调度。

## 当前棒位

| 项 | 值 |
|---|---|
| 章节 | ch-0001《至贱命格》(黄金五章版) |
| 当前节点 | **B2.3 — sc-0001-02〈旧契占理〉第 3 拍** |
| 前置状态 | sc-0001-01 已 pass；sc-0001-02 认知包已编；B2.1 沈砚、B2.2 柯九已入场记 |
| 下一棒角色 | 优先世界拍（镇差/旧契房道具）或沈砚回应柯九追问 |
| 下一 run-id | `relay/ch-0001/sc-0001-02-b03-world` 或 `sc-0001-02-b03-shen-yan.r1/` |
| 目标产物 | 给旧契房查卷增加程序压力，或让沈砚在不泄露超认知的前提下解释旧契熟悉来源；不能让旧契立即定案 |

## 下一步

1. 建议先走 B2.3 世界拍：镇差/旧契房道具给出压力（如柜钥、押印、账房规矩），让“查乙库”不至于立刻成功。
2. 若回沈砚：只递公开场记 Beat 1-2 的 SPEAK/ACT，不给柯九 INNER；让他解释旧契熟悉来源时保持“七年拓碑/跑腿见过”的凡俗边界。
3. 保持导演限制：小爽点只能是暂缓/逼退半步，不得彻底洗清危机。

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
| B2 | sc-0001-02 演绎 | 沈砚@gpt/deepseek stand-in / 柯九@antigravity 或 deepseek stand-in | `sc-0001-02-b*` | ▶️ b01✅ b02✅；b03 next |
| C2/W2 | sc-0001-02 验收+工作态 | checker+memory | `sc-0001-02-check/working` | pending |
| P3~W3 | sc-0001-03 夜半反痕 | 多 agent | `sc-0001-03-*` | pending |
| Z1 | 正文生成 | prose-writer@deepseek | `ch-0001-prose.r1` | pending |
| Z2~Z5 | 连续性/终审/记忆/发布前自检 | GPT/非同模评审/Cursor候选 | `ch-0001-*` | pending |

## 账本镜像

```
调度: { dispatch: 24, claude: 2, codex: 6, deepseek: 7, antigravity: 2, gemini: 2, cursor: 0, ollama: 6, retry: 6, 方式A: 1, 手动CLI: 18, 兼任: 1, stand_in: 4, 作废: 7 }
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

created_by: showrunner@codex via codex-main · handoff-board
