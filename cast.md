# cast.md · 选角表(角色 → 本机 CLI)

> 把每个角色指派给一个模型。**换模型只改这张表,不动 `roles/` 角色卡、不动任何文档。**
> 运行方式 B(推荐):Showrunner 按本表的"调用"列用 Bash 调度,协议见 `playbook/0-cli-relay.md`。
> 本机三通道:`claude`(Anthropic)| `codex`(OpenAI,OAuth)| `opencode`(DeepSeek,api-key)。

## 总控

| 角色 | 角色卡 | 通道 | 启动方式 |
|---|---|---|---|
| Showrunner | `roles/showrunner.md` | Claude Code 主会话 | `./run.sh`(或 `claude` 交互式)。只调度不创作,**任何角色都不在主会话里演** |

## 职能 Agent(有上帝视角,调度时 cwd=仓库根,可读其角色卡"输入"清单内文件)

| 角色 | 角色卡 | 模型 | 调用(见 playbook/0 §2 模板) | 选角理由 |
|---|---|---|---|---|
| 世界观架构师 | `roles/world-architect.md` | Claude | `claude -p` | 强一致性裁决 |
| 剧情导演 | `roles/plot-director.md` | GPT | `codex exec --sandbox read-only` | 结构与节奏 |
| 总编 | `roles/editor.md` | Claude | `claude -p` | 强推理、敢驳回;与正文 maker(DeepSeek)异模型 |
| 连续性检查器 | `roles/continuity-checker.md` | GPT | `codex exec --sandbox read-only` | 机械核对;与正文 maker(DeepSeek)异模型 |
| 小说输出器 | `roles/prose-writer.md` | DeepSeek | `opencode run -m deepseek/deepseek-chat` | 中文文采 |
| 记忆管理员 | `roles/memory-manager.md` | Claude | `claude -p` | 结构化稳定 |

> 模型号以本机实际为准:`opencode models`(确认 deepseek 型号)、`codex exec --help`、`claude --help`。
> 备用降级(限额/故障时):GPT→chatgpt.com 网页贴(方式A);DeepSeek→deepseek 网页贴;详见 playbook/0 §4。

## 角色演员(零上帝视角;调度时 cwd=run 目录,prompt 即全部世界,禁读文件)

| 角色 | slug | 角色卡 | 模型 | 调用 | 备注 |
|---|---|---|---|---|---|
| 男主·沈砚 | `shen-yan` | `roles/character-actor.md` | GPT | `codex exec --cd $P --sandbox read-only --skip-git-repo-check` | 沉静守拙、认死理 |
| 女主·苏决 | `su-jue` | `roles/character-actor.md` | DeepSeek | `(cd $P && opencode run -m deepseek/deepseek-chat …)` | 凌厉寡言、剑修 |
| 反派·柯九 | `ke-jiu` | `roles/character-actor.md` | Claude | `(cd $P && claude -p …)` | 和气健谈、藏钩子 |

三家演员=天然声音差异。新角色入册时在此表加行,按声线配模型。

## maker-checker 矩阵(§10 铁律2 的落地,发布前 I 组审计对照此表)

| 产物 | maker | checker(必须异模型) |
|---|---|---|
| 正文 `drafts/` | DeepSeek(输出器) | GPT(机械核对)→ Claude(终审) ✓ 三家全链异构 |
| 场记 `transcripts/` | 三家演员 | GPT(场景验收)+ Claude(总编抽检) |
| 章纲/brief `story/` | GPT(导演) | Claude(终审) ✓ |
| 认知包 `context_packs/` | Claude(记忆) | GPT(场景验收的隔离审计) ✓ |
| 记忆补丁 `memory/` | Claude(记忆) | Showrunner 回读校验(同模型,但 L3 是机械比对,可接受;存疑时人工逐条) |

> 总编(`claude -p` 子进程)与 Showrunner(Claude 主会话)同模型——满足"至少异会话"的底线;
> 终审驳回的是 DeepSeek 的正文与 GPT 的结构,不审自己的产出,无自产自审。

## 使用规矩

1. **一次调度=一个干净上下文**(无状态单次调用),天然不串味;绝不用 resume/session 续聊。
2. 每次调度 prompt 第一块永远是该角色的**角色卡全文**(无状态意味着每次都要带,见 playbook/0 §3)。
3. 一致性兜底永远是:世界以 `world/` 为准、记忆以 `memory/` 为准、过审以总编为准——与模型无关。
4. stand-in 需用户当场批准并计数;**评审角色绝不由"与 maker 同模型"者 stand-in**(playbook/0 §4 红线)。

## 换模型 / 加模型

- 换:改本表"模型"与"调用"两列即可,下次调度即生效。人设与记忆在文档里,连续性不丢。
- 加第四家(如本机再装新 CLI):在 playbook/0 §2 加一行命令模板,在本表选角即可。
