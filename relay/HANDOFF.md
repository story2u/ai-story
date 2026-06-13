# 接力板 · Codex 主控 / DeepSeek 主创

> **本板是 Showrunner 独占维护的唯一进度看板。**
> 当前作者指令(2026-06-13): Claude 额度用完，先冻结 Claude；由 Codex 当 Showrunner 主控，DeepSeek 当主创；
> Kiro / Antigravity / Cursor / Ollama 尽量参与共创。CLAUDE 保留主创角色但暂不启用。

## 当前通道实测

- Codex: `/Applications/Codex.app/Contents/Resources/codex` 可用；Homebrew `/opt/homebrew/bin/codex` 当前缺 vendor binary，不用。
- DeepSeek: `opencode` 可用，冒烟输出 `OK-deepseek`；当前作为主创/主要 stand-in 通道。
- Gemini/Antigravity: `gemini` 冒烟可用；B1.5 演员调用遇到模型容量耗尽，暂作不稳定通道。Antigravity.app 存在。
- Kiro: `kiro` 命令存在，但当前只确认是编辑器/应用入口，未确认可非交互输出角色交付物。
- Cursor: Cursor.app 存在；`cursor-agent` / `cursor` 当前不在 PATH，暂不能命令棒调用。
- Ollama: `ollama` 可用，已装 `qwen3.5:9b-q4_K_M`；短任务可用，长验收偏慢，调用时优先加 `--think=false --hidethinking`。
- Claude: 保留在 cast 里，但当前冻结，不调度。

## 当前棒位

| 项 | 值 |
|---|---|
| 章节 | ch-0001《至贱命格》(黄金五章版) |
| 当前节点 | **B2.2 — sc-0001-02〈旧契占理〉第 2 拍** |
| 前置状态 | sc-0001-01 已 pass；sc-0001-02 认知包已编；B2.1 沈砚已入场记 |
| 下一棒角色 | 优先 Ke Jiu（Gemini/Antigravity 若可用；否则 DeepSeek stand-in）或世界拍（镇差/旧契房道具） |
| 下一 run-id | `relay/ch-0001/sc-0001-02-b02-ke-jiu.r1/` 或 `sc-0001-02-b02-world` |
| 目标产物 | 推动柯九旁敲侧击或镇差/旧契房压力，不能让旧契立即定案 |

## 下一步

1. 组装 B2.2 prompt：只递给柯九其私有认知包、公开场记 Beat 1 的 SPEAK/ACT，不给沈砚 INNER。
2. 若 Gemini/Antigravity 仍不可用，按作者“DeepSeek 主创”指令启用 DeepSeek stand-in，产物标注并计账。
3. B2.2 目标：让柯九不直接帮忙、不出手，只用闲话把“沈砚为何这么熟旧契”这点钩出来；或由世界拍让镇差/账房给出压力。

## ch-0001 节点图

| # | 节点 | 角色@模型 | run-id | 状态 |
|---|---|---|---|---|
| D2 | 黄金前五章重设计 | plot-director@gpt | `arc-01-golden5-redesign.r1` | ✅ done，作者确认 |
| P1 | sc-0001-01 认知包 | memory-manager@claude(兼任) | `sc-0001-01-packs.r2` | ✅ done |
| B1 | sc-0001-01 演绎 | 沈砚@gpt / 柯九@gemini+deepseek stand-in | `sc-0001-01-b*` | ✅ done，6 beats |
| L0 | b1-b4 拍抽检 | editor-spotcheck@deepseek | `sc-0001-01-spotcheck-b01-b04.r1` | ✅ pass |
| C1 | sc-0001-01 场景验收 | continuity-checker@gpt | `sc-0001-01-check.r1` | ✅ pass |
| W1 | sc-0001-01 工作态 | memory-manager@ollama | `sc-0001-01-working-memory.r1` | ✅ done |
| P2 | sc-0001-02 认知包 | memory-manager@ollama/deepseek | `sc-0001-02-packs.r1` | ✅ done：Ollama 超时；DeepSeek r3 accepted |
| B2 | sc-0001-02 演绎 | 沈砚@gpt/deepseek stand-in / 柯九@gemini 或 deepseek stand-in | `sc-0001-02-b*` | ▶️ b01✅；b02 next |
| C2/W2 | sc-0001-02 验收+工作态 | checker+memory | `sc-0001-02-check/working` | pending |
| P3~W3 | sc-0001-03 夜半反痕 | 多 agent | `sc-0001-03-*` | pending |
| Z1 | 正文生成 | prose-writer@deepseek | `ch-0001-prose.r1` | pending |
| Z2~Z5 | 连续性/终审/记忆/发布前自检 | GPT/非同模评审/Cursor候选 | `ch-0001-*` | pending |

## 账本镜像

```
调度: { dispatch: 20, claude: 2, codex: 6, deepseek: 7, gemini: 2, cursor: 0, ollama: 4, retry: 5, 方式A: 1, 手动CLI: 14, 兼任: 1, stand_in: 4, 作废: 6 }
```

## 最近历史

- 2026-06-13 保存 Claude 遗留进度并提交推送: `8d2b9e1 chore: save claude story progress`。
- 2026-06-13 B1.4 沈砚输出已入场记；L0 抽检通过。
- 2026-06-13 B1.5 Gemini 演员调用因容量失败；DeepSeek stand-in r1 越界引用“上一回开封”作废，r2 通过并入场记。
- 2026-06-13 B1.6 世界拍按 brief 收场，命中 sc-0001-01 exit conditions。
- 2026-06-13 sc-0001-01 L1 验收通过；Ollama 生成工作态，经 Showrunner 清理控制字符与未注册 fs-0003 后落盘。
- 2026-06-13 P2 认知包完成：Ollama 超时中断；DeepSeek stand-in r1 因沈砚包泄露柯九真相作废，r2 因未授权硬事实作废，r3 经 Showrunner 格式清理后落盘。
- 2026-06-13 B2.1 沈砚首拍完成：Codex CLI 额度耗尽（提示 2026-06-14 01:56 后可再试），DeepSeek stand-in 输出七字段合格，已入场记。下一棒 B2.2。

created_by: showrunner@codex via codex-main · handoff-board
