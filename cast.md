# cast.md · 选角表(角色 → 通道)

> 把每个角色指派给一个模型。**换模型只改这张表,不动 `roles/` 角色卡、不动任何文档。**
> 运行方式 M(当前,作者拍板):Showrunner 组 prompt/校验/落盘/记账,**作者在 Mac 手动执行命令或粘贴**,
> 协议见 `playbook/0-cli-relay.md` + `relay/HANDOFF.md`(接力板)。
> 当前编组(ad-2026-06-13-04):Codex 主控;DeepSeek 主创;Kiro / Antigravity / Cursor Agent / Ollama 共创;
> Claude 保留主创候补身份,但**冻结不启用**。
> 本机通道:Codex 主会话(Showrunner)| `/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex`(GPT,OAuth)|
> `opencode`(DeepSeek,api-key)| NVIDIA API `deepseek-ai/deepseek-v4-flash`(备用)| `kiro-cli chat --no-interactive`(Kiro)| `agy -p`(Antigravity)|
> `agent -p`(Cursor Agent)| `ollama run --think=false --hidethinking minimax-m3:cloud`| `claude`(冻结;作者解除冻结前不调度)。

## 总控

| 角色 | 角色卡 | 通道 | 启动方式 |
|---|---|---|---|
| Showrunner | `roles/showrunner.md` | Codex 主会话 | 只调度不创作;不兼任演员、正文、评审或记忆;所有角色产物走下表通道或作者批准的 stand-in |

## 职能 Agent(有上帝视角;CLI 调度时 cwd=仓库根,可读其角色卡"输入"清单内文件)

| 角色 | 角色卡 | 模型 | 调用 | 选角理由/备注 |
|---|---|---|---|---|
| 世界观架构师 | `roles/world-architect.md` | Kiro | `kiro-cli chat --no-interactive "$(cat $P/prompt.md)" > $P/out.md` | 世界搭建与设定协调;从 Claude 兼任改派(ad-2026-06-13-01) |
| 剧情导演 | `roles/plot-director.md` | GPT | `/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex exec --sandbox read-only --output-last-message $P/out.md "$(cat $P/prompt.md)"` | 结构与节奏 |
| 总编 | `roles/editor.md` | Cursor Agent | `agent -p --mode=ask --trust "$(cat $P/prompt.md)" > $P/out.md` | 与正文 maker(DeepSeek)、核对(GPT)异模型;承担终审与跨模型痕迹审计；prompt 必须声明只评不改 |
| 连续性检查器 | `roles/continuity-checker.md` | GPT | `/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex exec --sandbox read-only --output-last-message $P/out.md "$(cat $P/prompt.md)"` | 机械核对;与正文 maker 异模型 |
| 小说输出器 | `roles/prose-writer.md` | DeepSeek | `opencode run -m deepseek/deepseek-chat` | 中文文采；备用 NVIDIA API: `deepseek-ai/deepseek-v4-flash` |
| 记忆管理员 | `roles/memory-manager.md` | Ollama(MiniMax M3) | `ollama run --think=false --hidethinking minimax-m3:cloud "$(cat $P/prompt.md)" > $P/out.md` | 结构化维护;认知包仍受 GPT 隔离审计(异模型)。Kiro 为备用 |
| 发布自检员(轻量·新) | `checklists/pre-publish.md` 即任务卡 | Cursor Agent | `agent -p --mode=ask --trust "$(cat $P/prompt.md)" > $P/out.md` | I 组跨模型痕迹审计由独立通道核查;每章一次,轻量；prompt 必须声明只读检查 |

> 模型号/CLI 以本机实际为准:`opencode models`、`/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex exec --help`、`kiro-cli chat --list-models`、`agy models`、`ollama list`、`agent --help`、`agent models`。
> NVIDIA API 评估(2026-06-13):`deepseek-ai/deepseek-v4-flash` 冒烟成功;`NVIDIA_API_KEY` 在 `.zshrc`,调度需 `zsh -ic` 或显式 source;high thinking 简单请求约 60s,仅作备用/高推理通道。
> 备用降级(限额/故障时):各模型网页/App 粘贴(方式A);详见 playbook/0 §4。
> Claude 冻结期不作为默认备用或 stand-in;只有作者明确解除冻结并更新本表/接力板后才可调度。
> Ollama 评估(2026-06-13):`kimi-k2.6:cloud` 返回 403 subscription required;`minimax-m3:cloud` 约 2.45s 冒烟成功。调用时必须加 `--think=false --hidethinking`。

## 角色演员(零上帝视角;prompt 即全部世界,禁读文件禁用工具)

| 角色 | slug | 角色卡 | 模型 | 调用 | 备注 |
|---|---|---|---|---|---|
| 男主·沈砚 | `shen-yan` | `roles/character-actor.md` | GPT | `/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex exec --cd $P --sandbox read-only --skip-git-repo-check --output-last-message $P/out.md "$(cat $P/prompt.md)"` | 沉静守拙、认死理 |
| 女主·苏决 | `su-jue` | `roles/character-actor.md` | DeepSeek | `(cd $P && opencode run -m deepseek/deepseek-chat …)` | 凌厉寡言、剑修 |
| 反派·柯九 | `ke-jiu` | `roles/character-actor.md` | **Antigravity(GPT-OSS 120B)** | `(cd $P && agy --model "GPT-OSS 120B (Medium)" -p "$(cat prompt.md)" > out.md)` | 和气健谈、藏钩子;自 Claude 改派;Gemini 已卸载不再使用 |

三家演员(GPT/DeepSeek/Antigravity)=天然声音差异,全异模型。新角色入册时在此表加行,按声线配模型
(Kiro/Antigravity/Cursor Agent/Ollama 可作新演员或职能通道候选;Claude 冻结期不入候选池)。

## 冻结候补

| 角色/能力 | 模型 | 状态 | 启用条件 |
|---|---|---|---|
| 主创候补 / 高阶审稿 / 复杂设定裁决 | Claude | **保留但不启用** | 作者明确解除冻结,并同步修改本表、`AGENTS.md`/`CLAUDE.md` 与 `relay/HANDOFF.md` |

## maker-checker 矩阵(§10 铁律2 的落地,发布前 I 组审计对照此表)

| 产物 | maker | checker(必须异模型) |
|---|---|---|
| 正文 `drafts/` | DeepSeek(输出器) | GPT(机械核对)→ Cursor Agent(总编) ✓ |
| 场记 `transcripts/` | 三家演员(GPT/DeepSeek/Antigravity) | GPT(场景验收)+ Cursor Agent(总编抽检) |
| 章纲/brief `story/` | GPT(导演) / Kiro(架构师) | Cursor Agent(总编) ✓ |
| 认知包 `context_packs/` | Ollama/MiniMax(记忆) | GPT(场景验收的隔离审计) ✓ 异模型 |
| 记忆补丁 `memory/` | Ollama/MiniMax(记忆) | Codex Showrunner 回读校验;存疑时改派 GPT 抽查或作者人工 |
| 发布前自检 | Codex Showrunner 自查 | **Cursor Agent(发布自检员)复核** ✓ 独立通道 |

> Codex 是主控而非 maker/checker;若某一步产物由 `codex exec` 生成,其 checker 不得再用 GPT/Codex 通道。
> Claude 冻结期不参与 maker-checker 链路,账本中 `claude` 应为 0。

## 使用规矩

1. **一次调度=一个干净上下文**:CLI 单次调用,或 IDE 型 agent(Kiro/Antigravity/Cursor Agent)的**全新会话**;绝不续聊。
2. 每次调度 prompt 第一块永远是该角色的**角色卡全文**(无状态意味着每次都要带,见 playbook/0 §3)。
3. **无默认兼任**:Codex Showrunner 不代写任何角色交付物。确需 stand-in 时必须作者当场批准、产物如实标注、账本计数。
4. **演员棒走粘贴通道时**(Kiro/Antigravity/Cursor Agent):作者开**不挂载本仓库的干净新会话**,粘 prompt.md 全文,
   把输出存回 `relay/<ch>/<run-id>/out.md`(或贴回 Codex Showrunner 落盘);账本计 `方式A`。
5. 一致性兜底永远是:世界以 `world/` 为准、记忆以 `memory/` 为准、过审以总编为准——与模型无关。
6. stand-in 需作者当场批准并计数;**评审角色绝不由"与 maker 同模型"者 stand-in**(playbook/0 §4 红线)。
   Claude 冻结期不作为 stand-in;Cursor Agent 已是总编/发布自检时,不得再审自己生成的产物。

## 换模型 / 加模型

- 换:改本表"模型"与"调用"两列即可,下次调度即生效。人设与记忆在文档里,连续性不丢。
- 加:在 playbook/0 §2 加一行命令模板(无 CLI 的 IDE 型 agent 走"干净新会话粘贴"),在本表选角即可。

created_by: showrunner@codex via codex-main · cast-r7(ad-2026-06-13-04)
