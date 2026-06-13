# 任务：ch-0001 发布前自检 r1

你是发布自检员。只评不改；不要写文件，不要执行命令；只输出 markdown 报告到 stdout。
按 checklists/pre-publish.md 逐组 A-I 判定 pass/fail；重点 H 循环卫生、I 跨模型痕迹审计。
报告名 reviews/ch-0001.pre-publish.r1.md。最后给 VERDICT: pass | fail；BLOCKERS；WARNINGS；REPORT。

## 自检清单

# 发布前自检清单（替代代码校验 · 手动过一遍）

> 在 `playbook/6-review-commit.md` 提交前逐项打勾。任何一项不过 → 回退，别发布。

## A. 信息隔离审计（最重要）
- [ ] 本章每个角色的认知包里，**没有**它不该知道的秘密 / 别人的 INNER / 它不在场发生的事。
- [ ] 演绎接力时，没有把别的角色的认知包或 INNER 粘进某角色的窗口。
- [ ] 每个角色用的是各自独立、干净的会话（无串演）。
- [ ] 新事件的 `known_by` 设置正确——不该知道的角色没被列入，避免信息"泄漏"到下一章。

## B. 连续性（对照 continuity 报告）
- [ ] 上一章结尾与本章开头衔接得上（时间/地点/在场人物/未完动作）。
- [ ] 道具/功法/信物的"有没有"与 `memory/character-state.md` 一致。
- [ ] 角色移动距离/耗时符合 `world/geography.md`；时间线无倒错。
- [ ] 称谓、伤势、情绪延续；离场/death 者未乱入。

## C. 设定与战力（对照 editorial 报告）
- [ ] 无违背 `world/rules.md` 铁则/禁忌。
- [ ] 战力对照 `world/power-system.md` 压制关系，无未解释越级。
- [ ] 涉及世界规则变更的，已有架构师 `approve`。

## D. 人物与逻辑
- [ ] 无 OOC（每个关键决定都能追溯到人设与已知信息）。
- [ ] 每个转折有动机与铺垫，无"为推进而推进"。

## E. 伏笔与线索
- [ ] 本章该回收的伏笔已回收；新埋的已登记进 `memory/foreshadowing.md`。
- [ ] 开启/关闭的线索已更新 `memory/threads.md`。

## F. 正文边界
- [ ] 正文没有出现场记里没演过的情节/人物/设定（输出器未越权创作）。

## G. 记忆与归档
- [ ] `memory_patch` 已审阅并幂等应用到 `memory/*.md`，且**回读校验 verified**。
- [ ] `memory/working/<ch>.md`（章内工作态）已被正式 patch 取代并删除。
- [ ] 本章 `摘要` 已回填 `story/chapters/<ch>.md`。
- [ ] 写权限合规（各文件由对应角色产出，无越权）。

## H. 循环卫生（HARNESS §10）
- [ ] 每个场景都有验收 `pass` 报告（`reviews/<sc>.scene-check.r*.md`）。
- [ ] 每次回退都有落盘的 revision-brief（章/场级成文件，拍级内联场记）——没有"口头回退"。
- [ ] 回退轮次未超预算（单闸≤2、全章≤4）；若超，走的是**升级作者**而不是放水。
- [ ] 审报按轮次归档（`.r<N>`），`REPEAT` 项已记入 `memory/lessons.md`；同类第 2 次已硬化（或已列入弧线回顾待办）。
- [ ] 演员 prompt 从未收到审稿证据原文 / lessons 内容（只收"作废声明＋新本拍指令"）。

## I. 跨模型痕迹审计（playbook/0 · 防"单模型代演"回潮）
- [ ] 本章关键产物（章纲/场记各拍/正文/两份审报/认知包/patch）都有 `created_by: <角色>@<模型> via <cli> · <run-id>` 戳，
      且与 `cast.md` 选角一致；`relay/<ch>/` 下能找到对应 run 留痕。
- [ ] **maker ≠ checker（异模型）**：正文(DeepSeek)→机械核对(Kiro/GPT 等非 DeepSeek)→终审(Cursor Agent)；场记(演员/世界拍)→验收(与 maker 异模型)。对照 cast.md 矩阵逐条核。
- [ ] 调度账本已记入章文件"流水线状态"；`stand_in = 0`，或每次 stand-in 都有"用户当场批准"的记录＋作者签字放行。
- [ ] 没有任何评审产物出自"与被审产物 maker 同模型"的 stand-in。
- [ ] 演员各 run 的 prompt 抽查 2 个：不含仓库路径、不含他人 INNER/认知包、不含该角色不在场的拍。

全绿 → `git add … && git commit -m "feat(<ch>): <标题>"`。


## cast.md

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


## 章节状态

---
id: ch-0001
arc: arc-01
target_words: 3200
title: 至贱命格
---

# 章节大纲 · ch-0001

## 大纲（要发生什么）
开篇不从日常慢铺，而从开封前的清册复核切入。碑亭镇临近开封，镇里按旧规清点命牌、役籍与碑林出入人。沈砚正在无字碑林做拓碑活，忽被镇差当众点出「至贱命格」，要求他交出随身旧砚、暂离碑林，以免冲撞开封清册。

乔装成游方修士的柯九在场，他表面看热闹，暗中顺势试探：这个被人轻贱的少年，是否就是「上头」要找的命格异常者。沈砚不知内情，只知道旧砚是自己的东西，碑林活计也是自己凭手艺挣来的。他不逞强、不动怒，只死死抓住一条旧规：镇里要夺物、禁人，得有明白来由，得拿得出章程。

镇差拿不出足够凭据，沈砚却也被迫暴露出两件事：他对碑林旧契极熟，且那方旧砚在争执中出现一瞬难以解释的微温。柯九没有当场动手，却把沈砚记成重点。入夜，沈砚回到破屋，拓纸上多出一枚他看不懂的暗痕，像是从无字碑背面反拓出来的残印。本章以沈砚意识到「今天这事没有完」收钩。

## 场景清单
- sc-0001-01 — 清册点名：沈砚在碑林当众被至贱命格压住，柯九旁观试探。
- sc-0001-02 — 旧契占理：沈砚借碑林旧契逼镇差退半步，柯九确认他值得深查。
- sc-0001-03 — 夜半反痕：沈砚独处时旧砚微温，拓纸显出不可解的暗痕。

## 本章钩子
夜里，沈砚本想把白日的事压下去，却发现白纸上多出一枚并非他拓出的暗痕；与此同时，白日那位和气的柯先生，已经把他的名字记进了另一份看不见的清单。

## 风格
见 `drafts/STYLE.md`。本章贴沈砚限知为主，短切柯九视角制造读者信息差。节奏要快：第一场即给危机，第二场给沈砚「以理逼退」的小爽点，第三场留悬疑钩。世界观信息只通过清册、旧契、命格歧视与碑林异象露出，不做说明书。

## 摘要
清册复核当日，沈砚在无字碑林边被镇差当众点出「至贱命格」，要求交出随身旧砚并暂离碑林。沈砚没有硬抗，只追问押印、归还与旧规章程；乔装游方修士的柯九在旁看似帮腔，实则借话试探旧砚、七年拓碑与沈砚反应。争执被逼往镇衙旧契房后，沈砚凭自己熟悉的旧契房程序指向乙库，经手簿与底册证明旧砚并非贼赃私匿，镇差只能退半步，让旧砚暂归沈砚照管，但留下三日复核、旧砚不得离身外借、沈砚不得擅离碑亭镇的后续压力。入夜后，沈砚独处发现旧砚微温、拓纸自变，并在拓纸右下角看见残缺凹痕与铅灰细迹；他无法解释，只将旧砚与拓纸分藏，决定明日侧查旧例。同夜，柯九把沈砚列为重点观察对象，准备借三日复核窗口深查经手簿与乙库残卷。

## 流水线状态（/chapter 维护，断点续跑用 · 循环账本 schema 见 playbook/chapter-pipeline.md）
- **v2 重制·黄金前五章版**：旧设计(v1 起草、D1 复核版)已被 D2(arc-01-golden5-redesign.r1)取代，作者确认 2026-06-12。
  v1 产物归档于 `*/v1/`；运行方式=方式 M(接力板 `relay/HANDOFF.md`)。
- 设计: done——D2 重设计+作者确认；本章 3 场 brief 已落盘
- 断点: ch-0001 complete——正文已生成，连续性/总编/记忆回读均通过；下一入口为 ch-0002 P1。
- 演绎: { sc-0001-01: done·验收pass(r1), sc-0001-02: done·验收pass(r1), sc-0001-03: done·验收pass(r1) }
- 正文: done·drafts/ch-0001.md·prose r2
- 连续性: pass(r2) ｜ 终审: pass(r2) ｜ 记忆: patch-applied·verified(r1)·working-deleted
- 调度: { dispatch: 57, claude: 2, codex: 11, deepseek: 13, nvidia: 1, antigravity: 4, kiro: 7, gemini: 2, cursor: 3, ollama: 16, retry: 9, 方式A: 1, 手动CLI: 51, 兼任: 1, stand_in: 4, 作废: 7 }
- 回退累计: 1/4（prose r1→r2：追溯错字/物件位置/未登记 NPC 私名；editorial r1→r2：地名青槐镇→碑亭镇）
- 已发布: true

created_by: plot-director@gpt via codex(手动CLI) · arc-01-golden5-redesign.r1（作者确认 2026-06-12）
updated_by: showrunner@codex via codex-main · sc-0001-01-closeout
updated_by: showrunner@codex via codex-main · sc-0001-02-b01
updated_by: showrunner@codex via codex-main · sc-0001-02-b02
updated_by: showrunner@codex via codex-main · sc-0001-02-b03-world
updated_by: showrunner@codex via codex-main · sc-0001-02-b04
updated_by: showrunner@codex via codex-main · sc-0001-02-b05-loop
updated_by: showrunner@codex via codex-main · sc-0001-02-b06
updated_by: showrunner@codex via codex-main · sc-0001-02-closeout
updated_by: showrunner@codex via codex-main · sc-0001-03-closeout
updated_by: showrunner@codex via codex-main · ch-0001-prose-review-memory-complete


## 接力板

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
| 前置状态 | ch-0001 正文完成；连续性 pass(r2)；总编 pass(r2)；memory patch verified；`memory/working/ch-0001.md` 已删除 |
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
| Z1 | 正文生成 | prose-writer@deepseek | `ch-0001-prose.r1/r2` | ✅ done，r2 accepted |
| Z2~Z5 | 连续性/终审/记忆/发布前自检 | Kiro/Cursor/Kiro | `ch-0001-*` | ✅ continuity pass(r2)，editorial pass(r2)，memory verified |

## 账本镜像

```
调度: { dispatch: 57, claude: 2, codex: 11, deepseek: 13, nvidia: 1, antigravity: 4, kiro: 7, gemini: 2, cursor: 3, ollama: 16, retry: 9, 方式A: 1, 手动CLI: 51, 兼任: 1, stand_in: 4, 作废: 7 }
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

created_by: showrunner@codex via codex-main · handoff-board


## 关键产物索引

context_packs/.gitkeep
context_packs/sc-0001-01.ke-jiu.md
context_packs/sc-0001-01.shen-yan.md
context_packs/sc-0001-02.ke-jiu.md
context_packs/sc-0001-02.shen-yan.md
context_packs/sc-0001-03.ke-jiu.md
context_packs/sc-0001-03.shen-yan.md
context_packs/v1/sc-0001-01.ke-jiu.md
context_packs/v1/sc-0001-01.shen-yan.md
context_packs/v1/sc-0001-02.shen-yan.md
context_packs/v1/sc-0002-01.shen-yan.md
context_packs/v1/sc-0002-02.ke-jiu.md
context_packs/v1/sc-0002-03.su-jue.md
drafts/STYLE.md
drafts/ch-0001.md
drafts/v1/ch-0001.md
drafts/v1/ch-0002.md
memory/patches/.gitkeep
memory/patches/ch-0001.patch.md
memory/patches/v1/ch-0001.patch.md
memory/patches/v1/ch-0002.patch.md
relay/ch-0001/ch-0001-continuity.r1/out.md
relay/ch-0001/ch-0001-continuity.r1/out.raw.md
relay/ch-0001/ch-0001-continuity.r1/prompt.md
relay/ch-0001/ch-0001-continuity.r1/report.clean.md
relay/ch-0001/ch-0001-continuity.r2/out.md
relay/ch-0001/ch-0001-continuity.r2/out.raw.md
relay/ch-0001/ch-0001-continuity.r2/prompt.md
relay/ch-0001/ch-0001-continuity.r2/report.clean.md
relay/ch-0001/ch-0001-continuity.r2/revision-brief.md
relay/ch-0001/ch-0001-design-review.r1/out.md
relay/ch-0001/ch-0001-design-review.r1/prompt.md
relay/ch-0001/ch-0001-editorial.r1/out.md
relay/ch-0001/ch-0001-editorial.r1/out.raw.md
relay/ch-0001/ch-0001-editorial.r1/prompt.md
relay/ch-0001/ch-0001-editorial.r2/out.md
relay/ch-0001/ch-0001-editorial.r2/out.raw.md
relay/ch-0001/ch-0001-editorial.r2/prompt.md
relay/ch-0001/ch-0001-editorial.r2/revision-brief.md
relay/ch-0001/ch-0001-memory-patch.r1/out.raw.md
relay/ch-0001/ch-0001-memory-patch.r1/prompt.md
relay/ch-0001/ch-0001-memory-patch.r2-kiro/out.md
relay/ch-0001/ch-0001-memory-patch.r2-kiro/out.raw.md
relay/ch-0001/ch-0001-memory-patch.r2-kiro/patch.clean.md
relay/ch-0001/ch-0001-memory-patch.r2-kiro/prompt.md
relay/ch-0001/ch-0001-prepublish.r1/prompt.md
relay/ch-0001/ch-0001-prose.r1/out.md
relay/ch-0001/ch-0001-prose.r1/out.raw.md
relay/ch-0001/ch-0001-prose.r1/prompt.md
relay/ch-0001/ch-0001-prose.r2/out.md
relay/ch-0001/ch-0001-prose.r2/out.raw.md
relay/ch-0001/ch-0001-prose.r2/prompt.md
relay/ch-0001/ch-0001-prose.r2/revision-brief.md
relay/ch-0001/sc-0001-01-b01-shen-yan.r1/out.md
relay/ch-0001/sc-0001-01-b01-shen-yan.r1/prompt.md
relay/ch-0001/sc-0001-01-b03-ke-jiu.r1/out.md
relay/ch-0001/sc-0001-01-b03-ke-jiu.r1/prompt.md
relay/ch-0001/sc-0001-01-b04-shen-yan.r1/out.md
relay/ch-0001/sc-0001-01-b04-shen-yan.r1/prompt.md
relay/ch-0001/sc-0001-01-b05-ke-jiu.r1/out.md
relay/ch-0001/sc-0001-01-b05-ke-jiu.r1/out.r2.standin-deepseek.md
relay/ch-0001/sc-0001-01-b05-ke-jiu.r1/out.standin-deepseek.md
relay/ch-0001/sc-0001-01-b05-ke-jiu.r1/prompt.md
relay/ch-0001/sc-0001-01-b05-ke-jiu.r1/prompt.r2.md
relay/ch-0001/sc-0001-01-check.r1/out.codex.md
relay/ch-0001/sc-0001-01-check.r1/out.md
relay/ch-0001/sc-0001-01-check.r1/out.r2.md
relay/ch-0001/sc-0001-01-check.r1/prompt.codex.md
relay/ch-0001/sc-0001-01-check.r1/prompt.md
relay/ch-0001/sc-0001-01-packs.r1/out.md
relay/ch-0001/sc-0001-01-packs.r1/prompt.md
relay/ch-0001/sc-0001-01-spotcheck-b01-b04.r1/out.md
relay/ch-0001/sc-0001-01-spotcheck-b01-b04.r1/out.ollama.md
relay/ch-0001/sc-0001-01-spotcheck-b01-b04.r1/prompt.md
relay/ch-0001/sc-0001-01-working-memory.r1/out.md
relay/ch-0001/sc-0001-01-working-memory.r1/prompt.md
relay/ch-0001/sc-0001-02-b01-shen-yan.r1/out.standin-deepseek.md
relay/ch-0001/sc-0001-02-b01-shen-yan.r1/prompt.md
relay/ch-0001/sc-0001-02-b02-ke-jiu.r1/out.md
relay/ch-0001/sc-0001-02-b02-ke-jiu.r1/out.r2.md
relay/ch-0001/sc-0001-02-b02-ke-jiu.r1/prompt.md
relay/ch-0001/sc-0001-02-b02-ke-jiu.r1/prompt.r2.md
relay/ch-0001/sc-0001-02-b04-shen-yan.r1/out.md
relay/ch-0001/sc-0001-02-b04-shen-yan.r1/prompt.md
relay/ch-0001/sc-0001-02-b05-world-check.r1/out.md
relay/ch-0001/sc-0001-02-b05-world-check.r1/prompt.md
relay/ch-0001/sc-0001-02-b05-world-ruling.r1/out.md
relay/ch-0001/sc-0001-02-b05-world-ruling.r1/prompt.md
relay/ch-0001/sc-0001-02-b05-world.r1/out.md
relay/ch-0001/sc-0001-02-b05-world.r1/prompt.md
relay/ch-0001/sc-0001-02-b06-ke-jiu-check.r1/out.md
relay/ch-0001/sc-0001-02-b06-ke-jiu-check.r1/prompt.md
relay/ch-0001/sc-0001-02-b06-ke-jiu.r1/out.md
relay/ch-0001/sc-0001-02-b06-ke-jiu.r1/prompt.md
relay/ch-0001/sc-0001-02-b07-world-check.r1/out.md
relay/ch-0001/sc-0001-02-b07-world-check.r1/prompt.md
relay/ch-0001/sc-0001-02-b07-world.r1/out.md
relay/ch-0001/sc-0001-02-b07-world.r1/prompt.md
relay/ch-0001/sc-0001-02-check.r1/out.md
relay/ch-0001/sc-0001-02-check.r1/prompt.md
relay/ch-0001/sc-0001-02-packs.r1/out.md
relay/ch-0001/sc-0001-02-packs.r1/out.r2.standin-deepseek.md
relay/ch-0001/sc-0001-02-packs.r1/out.r3.standin-deepseek.md
relay/ch-0001/sc-0001-02-packs.r1/out.standin-deepseek.md
relay/ch-0001/sc-0001-02-packs.r1/prompt.md
relay/ch-0001/sc-0001-02-packs.r1/prompt.r2.md
relay/ch-0001/sc-0001-02-packs.r1/prompt.r3.md
relay/ch-0001/sc-0001-02-spotcheck-b01-b04.r1/out.md
relay/ch-0001/sc-0001-02-spotcheck-b01-b04.r1/prompt.md
relay/ch-0001/sc-0001-02-working-memory.r1/out.md
relay/ch-0001/sc-0001-02-working-memory.r1/prompt.md
relay/ch-0001/sc-0001-03-b01-shen-yan.r1/out.md
relay/ch-0001/sc-0001-03-b01-shen-yan.r1/prompt.md
relay/ch-0001/sc-0001-03-b02-world-check.r1/out.md
relay/ch-0001/sc-0001-03-b02-world-check.r1/prompt.md
relay/ch-0001/sc-0001-03-b02-world.r1/out.md
relay/ch-0001/sc-0001-03-b02-world.r1/prompt.md
relay/ch-0001/sc-0001-03-b03-shen-yan.r1/out.md
relay/ch-0001/sc-0001-03-b03-shen-yan.r1/prompt.md
relay/ch-0001/sc-0001-03-b04-world-check.r1/out.md
relay/ch-0001/sc-0001-03-b04-world-check.r1/prompt.md
relay/ch-0001/sc-0001-03-b04-world.r1/out.md
relay/ch-0001/sc-0001-03-b04-world.r1/prompt.md
relay/ch-0001/sc-0001-03-b05-shen-yan.r1/out.md
relay/ch-0001/sc-0001-03-b05-shen-yan.r1/prompt.md
relay/ch-0001/sc-0001-03-b06-ke-jiu.r1/out.md
relay/ch-0001/sc-0001-03-b06-ke-jiu.r1/prompt.md
relay/ch-0001/sc-0001-03-packs.r1/out.md
relay/ch-0001/sc-0001-03-packs.r1/prompt.md
relay/ch-0001/sc-0001-03-scene-check.r1/out.md
relay/ch-0001/sc-0001-03-scene-check.r1/out.raw.md
relay/ch-0001/sc-0001-03-scene-check.r1/prompt.md
relay/ch-0001/sc-0001-03-spotcheck-b01-b06.r1/out.md
relay/ch-0001/sc-0001-03-spotcheck-b01-b06.r1/prompt.md
relay/ch-0001/sc-0001-03-working-memory.r1/out.clean.md
relay/ch-0001/sc-0001-03-working-memory.r1/out.md
relay/ch-0001/sc-0001-03-working-memory.r1/prompt.md
reviews/.gitkeep
reviews/ch-0001.continuity.r1.md
reviews/ch-0001.continuity.r2.md
reviews/ch-0001.editorial.r1.md
reviews/ch-0001.editorial.r2.md
reviews/ch-0001.memory-verify.r1.md
reviews/sc-0001-01.scene-check.r1.md
reviews/sc-0001-02.scene-check.r1.md
reviews/sc-0001-03.scene-check.r1.md
reviews/v1/ch-0001.continuity.r1.md
reviews/v1/ch-0001.editorial.r1.md
reviews/v1/ch-0001.editorial.r2.md
reviews/v1/ch-0002.continuity.r1.md
reviews/v1/ch-0002.editor.r1.md
reviews/v1/rb-ch-0001-r1.md
reviews/v1/rb-sc-0001-01-r1.md
reviews/v1/sc-0001-01.scene-check.r1.md
reviews/v1/sc-0001-01.scene-check.r2.md
reviews/v1/sc-0001-02.scene-check.r1.md
reviews/v1/sc-0002-01.scene-check.r1.md
reviews/v1/sc-0002-02.scene-check.r1.md
reviews/v1/sc-0002-03.scene-check.r1.md
transcripts/.gitkeep
transcripts/sc-0001-01.md
transcripts/sc-0001-02.md
transcripts/sc-0001-03.md
transcripts/v1/sc-0001-01.md
transcripts/v1/sc-0001-02.md
transcripts/v1/sc-0002-01.md
transcripts/v1/sc-0002-02.md
transcripts/v1/sc-0002-03.md


## 审核与验证报告

VERDICT: pass
ATTEMPT: r1
REDO_BEATS: []
ISOLATION: ok
REPORT: reviews/sc-0001-01.scene-check.r1.md
NOTES: [
- 导演限制守住：沈砚仅以“押印、归还、当众看验”抗辩，未识破柯九、未知旧砚真相、未显超凡；柯九只旁观拱火试探，未暴露细作身份/开府修为，未亲自夺砚。
- 收场合规：Beat 6 明确“沈砚暂时保住旧砚，却也被从碑林边逼向镇衙旧契房”，SCENE RESULT 同步写明“柯九确认沈砚值得继续盯，清册压力未解除”，命中 exit_conditions。
- 伏笔落地：fs-0001 在头部初始情境与 Beat 1/2 的当众“至贱命格”压迫中落地；fs-0002 在 Beat 1/3/4/5/6 的护砚、问砚、记砚链条中落地，且旧砚未发光、显字或回应碑林。
- 隔离审计通过：沈砚 Beats 1/4 的认知只来自公开压力与自身认知包；柯九 Beats 3/5 的“差事两件、排查命格被动过手脚”来自其认知包。B5 r1 越界信息已作废，r2 未再引用“上一回开封”。
]
created_by: continuity-checker@gpt via codex-app-cli · sc-0001-01-check.r1
VERDICT: pass
ATTEMPT: r1
REDO_BEATS: []
ISOLATION: ok
REPORT: reviews/sc-0001-02.scene-check.r1.md

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


# 场景验收报告 · sc-0001-02 旧契占理

│ 连续性检查器（Kiro/GLM-5）@ 2026-06-13 · r1

## 一、导演限制 · 逐条核对

| 限制 | 判定 | 证据 |
|---|---|---|
| 沈砚的胜利只能是「暂缓」「逼退半步」，不得彻底洗清危机 | ✅ 通过 | Beat 7：镇差"坚持旧契房只记用物去向，不议物主归属"，复核威胁保留（三日内持旧契复核、不得离身、不得离镇）；SCENE RESULT 明写"复核前旧砚不得离身、不得外借，沈砚亦不得擅离青槐镇" |
| 柯九不得替沈砚说话，也不得直接出手帮镇差 | ✅ 通过 | Beat 2、6：柯九仅以"闲聊试探""旁敲侧击"提问，未代沈砚争理，亦未助镇差夺砚；所有实质争理由沈砚自己完成 |
| 不得让旧契凭空包含世界级真相 | ✅ 通过 | Beat 5、7：旧契仅证明"做工时日吻合""旧砚来历确有凭据，非贼赃，非私匿"，无命格、封局、碑魂等超纲内容 |
| 不得出现苏决 | ✅ 通过 | 全场苏决未出场 |
| 不得让沈砚说出超出认知的推理 | ✅ 通过 | Beat 1、4：沈砚仅依据"七年拓碑、见过备案"推断乙库架位与旧规条款；未涉及命格改判、封局、碑魂等认知外概念 |

结论：5/5 限制守住，无违规。

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


## 二、收场合规 · exit_condition 命中核验

| exit_condition | 是否命中 | 证据 |
|---|---|---|
| 镇差暂不扣旧砚但留下后续复核/禁令威胁 | ✅ 命中 | Beat 7："旧砚暂归沈砚照管，三日内持旧契至镇衙复核，复核前旧砚不得离身、不得外借，沈砚亦不得擅离青槐镇" |
| 沈砚保住旧砚 | ✅ 命中 | Beat 7："将旧砚推过桌案半尺——未言归属，已许暂留" |
| 柯九确认沈砚与碑林旧契、旧砚都有可查价值 | ✅ 命中 | SCENE RESULT："柯九确认沈砚与旧契、旧砚都有可查价值" |

beat_budget：声明 12，实际使用 7（Beat 1-7），未超支。

emotional_target：声明"小爽点，弱者占理逼强势者退半步；爽后仍有更大危机"。
- ✅ Beat 5-7 提供爽点：沈砚以程序逼镇差退让，旧砚暂留。
- ✅ 危机延续：复核、禁离镇、旧具来历不闭环、柯九加深怀疑。

结论：收场合规，命中 exit_condition，预算未超，情绪目标达成。

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


## 三、伏笔落地 · 拍支撑核验

### fs-0001 · 清册与旧契之间存在不合常理的缝隙

支撑拍：
- Beat 5：账房翻出"碑林做活登记"与"旧具随工留用"两卷，"旧具来历栏空白，只记'随工交接'"——镇差"皱眉不语，随后翻出清册指给账房看，账房捋须摇头"。
- Beat 7：账房确认"旧砚来历确有凭据，非贼赃，非私匿"，但镇差"坚持旧契房只记用物去向，不议物主归属"——清册与旧契口径不闭环。

判定：✅ 有真实拍支撑，非仅 SCENE RESULT 声明。

### fs-0002 · 旧砚被保住，为夜间异痕做铺垫

支撑拍：
- Beat 7："旧砚暂归沈砚照管"——旧砚留在沈砚手中。
- SCENE RESULT："旧砚被保住并将带回夜间异痕"——后续伏笔铺垫成立。

判定：✅ 有真实拍支撑。

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


## 四、隔离审计 · 可见性与认知包核验

### 4.1 可见性标签核验

| Beat | 标签 | 是否合规 |
|---|---|---|
| Beat 1 | public | ✅ |
| Beat 2 | public | ✅ |
| Beat 3 | public（世界拍） | ✅ |
| Beat 4 | public | ✅ |
| Beat 5 | public（世界拍） | ✅ |
| Beat 6 | public | ✅ |
| Beat 7 | public（世界拍） | ✅ |

结论：全 public 标签正确。

### 4.2 认知包隔离核验

沈砚认知包（输入 3）：
- ✅ 不含柯九 INNER、旧砚真相、命格改判、碑魂。
- ✅ 含"你不知道的事：柯先生的来历与目的、清册背后是否有人设局"——盲区明确。

柯九认知包（输入 4）：
- ✅ 不含沈砚 INNER、旧砚真相、命格改判细节。
- ✅ 含"你不知道的事：旧契具体内容、沈砚命格真相、旧砚是否真有问题、旧砚真身来历"——盲区明确。

### 4.3 拍内 INNER 与 SPEAK/ACT 隔离

逐拍核验：
- **Beat 1（沈砚）**：INNER 含"乙库，二架三格"推测，SPEAK 仅说"乙库是碑林专档"——未暴露 INNER 具体位置推测，仅外显"对旧契房熟悉"。
- **Beat 2（柯九）**：INNER 含"试探沈砚对旧契房熟悉程度"，SPEAK 仅问"何时、何处熟悉这旧契房"——未暴露 INNER 探查意图。
- **Beat 4（沈砚）**：INNER 含"他（柯先生）这一问来得巧，像帮我，也像把我往火上添了一把"，SPEAK/ACT 仅向柯九"一揖"——未向柯九暴露怀疑。
- **Beat 6（柯九）**：INNER 含"从这缺口撬开线索"，SPEAK 仅问"谁曾将旧具递于此"——未暴露 INNER 探查意图。

结论：无 INNER 渗漏到 SPEAK/ACT。

### 4.4 是否有人说出未递信息

逐拍核验：
- **Beat 1（沈砚）**：说"乙库是碑林专档"，认知包确有"见过旧契房经手的备案盖印"—— ✅ 有依据。
- **Beat 4（沈砚）**：说"七年里我替人拓碑，拓成的纸、领过的纸墨、补过的押记，都要经旧契房的手"，认知包确有"七年来在无字碑林靠拓碑糊口"—— ✅ 有依据。
- **Beat 6（柯九）**：问"旧具一栏空白，却只记随工交接，这其中若有交接者的名号"，此信息来自 Beat 5 世界拍公开内容—— ✅ 有依据。

结论：无人说出未递信息。

### 4.5 SCENE RESULT 隔离自检核验

SCENE RESULT 声明：
│ 演员 prompt 仅递公开 SPEAK/ACT/WORLD_BEAT 与各自认知包；未向任何演员暴露他人 INNER、旧砚真相、命格改判真相、碑魂或不在场信息。

核验：
- ✅ 沈砚认知包无柯九 INNER、旧砚真相、命格真相。
- ✅ 柯九认知包无沈砚 INNER、旧砚真相、命格真相。
- ✅ 世界拍（Beat 3、5、7）仅记述程序与物理动作，无角色 INNER 外泄。

结论：自检属实。

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


## 五、综合判定

| 核对项 | 结果 |
|---|---|
| 导演限制 | 5/5 通过 |
| 收场合规 | ✅ 命中 exit_condition，预算未超，情绪目标达成 |
| 伏笔落地 | ✅ fs-0001 / fs-0002 均有真实拍支撑 |
| 隔离审计 | ✅ 无泄漏，可见性标签正确，认知包隔离有效 |

VERDICT: pass

ATTEMPT: r1

REDO_BEATS: []

ISOLATION: ok

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

created_by: continuity-checker@kiro/glm-5 via kiro-cli · reviews/sc-0001-02.scene-check.r1.md> # 场景验收报告 · sc-0001-03

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

report_id: sc-0001-03.scene-check.r1
scene: sc-0001-03
chapter: ch-0001
checker: continuity-checker@ollama/minimax-m3
attempt: r1
created: 2026-06-13T23:26:34+08:00
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


## 一、导演限制逐条核验

| 限制 | 守住？ | 证据 |
|---|---|---|
| 沈砚不得理解反痕含义，不得觉醒力量，不得与碑魂交流 | ✅ | Beat 3、5：沈砚明确"不懂这些"、"含义不明"；仅观察到物理现象，无觉醒/交流情节 |
| 异象必须极轻：旧砚微温、拓纸残痕、难以确认的碑林回应 | ✅ | Beat 2、4：旧砚"微温"、拓纸"凹痕"、"极淡铅灰"、碑林"极轻一声石响"；无文字/神祇/命格揭示 |
| 若切柯九，只能作为章尾信息差，不得让柯九看到沈砚夜间异象 | ✅ | Beat 6：柯九在"暗处""别处"，内容仅为整理线索、将沈砚列为重点；无沈砚夜间异象信息 |
| 不得出现苏决、阿公或其他复杂角色 | ✅ | 全场仅沈砚、柯九出场 |
| 沈砚不得主动制定超出认知的权谋大局 | ✅ | Beat 1、3、5：沈砚策略限于"守物、守规矩、明日侧查旧例"；无大局谋划 |

结论：导演限制全部守住。

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


## 二、收场合规

beat_budget：6 → 实际使用：6 拍 ✅

exit_conditions 检验：

| 条件 | 命中？ | 证据 |
|---|---|---|
| 沈砚发现反痕并生出更深不安 | ✅ | Beat 4-5：沈砚发现凹痕；Beat 5 INNER："这纸不对……白日那场事只怕还没落地"；SCENE RESULT："意识到白日风波没有结束" |
| 柯九将沈砚记为重点 | ✅ | Beat 6 INNER："沈砚已成我重点观察的对象"；SCENE RESULT："柯九把沈砚列为重点观察对象" |
| 章尾明确「此事未完」 | ✅ | SCENE RESULT outcome："沈砚……意识到白日风波没有结束"；柯九"准备借三日复核窗口深查" |

收场判断：命中多条 exit_conditions，beat_budget 未超，收束自然。 ✅

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


## 三、伏笔落地核验

| 伏笔 ID | 类型 | brief 声明 | 场记支撑 | 落地？ |
|---|---|---|---|---|
| fs-0002 | plant | 旧砚/拓纸/无字碑林的微弱感应 | Beat 2：旧砚微温、拓纸自变、碑林石响；Beat 4：残缺凹痕与铅灰细迹 | ✅ 有真实拍支撑 |
| fs-0001 | plant | 反痕与清册压迫形成暗线关联 | Beat 5 INNER："白日那场事只怕还没落地"；SCENE RESULT："清册压迫与旧契复核压力继续外推" | ✅ 语义关联已埋 |

结论：伏笔声明与场记一致，非空头声明。

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


## 四、隔离审计

### 4.1 可见性标签核验

| 拍号 | 角色 | 标签 | 正确？ | 理由 |
|---|---|---|---|---|
| Beat 1 | shen-yan | public | ✅ | 沈砚独处动作与内心，无柯九在场，公开即可 |
| Beat 2 | world-beat | public | ✅ | 世界拍为公共信息，所有角色可见（但沈砚实际在场，柯九不在） |
| Beat 3 | shen-yan | public | ✅ | 同 Beat 1 |
| Beat 4 | world-beat | public | ✅ | 同 Beat 2 |
| Beat 5 | shen-yan | public | ✅ | 同 Beat 1 |
| Beat 6 | ke-jiu | solo | ✅ | 柯九独处，沈砚不在场，solo 正确 |

标签使用正确。

### 4.2 隔离自检核验（SCENE RESULT 声明 vs 场记事实）

SCENE RESULT 声明：
│ 沈砚未获得柯九暗中建档、开府修为或上头任务信息；柯九未获得沈砚夜间亲见的旧砚微温、拓纸自变、残缺反痕细节。

核验：

- **沈砚获得柯九信息？** ❌ 未获得
  - Beat 1-5：沈砚场记中无任何柯九暗中建档/开府修为/上头任务的信息流入
  - 认知包"此刻不知"：明确列出"不知道柯九的真实来意与修为"

- **柯九获得沈砚夜间异象？** ❌ 未获得
  - Beat 6：柯九场记内容仅为整理白日线索、决定深查；无旧砚微温/拓纸自变/反痕细节
  - 认知包"此刻不知"：明确列出"不知道沈砚夜间独处时会做什么，也看不到沈砚住处"

结论：隔离自检声明属实，无泄露。 ✅

### 4.3 认知包盲区穿透检查

- 沈砚认知包"此刻不知"：命格真相、柯九真实来意与修为、柯九暗线任务、旧砚/拓纸/碑林玄机关联
  - 场记 Beat 1-5：均未向沈砚传递上述信息 ✅

- 柯九认知包"此刻不知"：命格真相、沈砚夜间行为、沈砚对柯九的提防、旧砚/碑林玄机实证
  - 场记 Beat 6：均未向柯九传递上述信息 ✅

结论：认知包盲区未被穿透。

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


## 五、问题清单

无 BLOCKER。

无 CRITICAL。

无 MINOR。

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


## 六、总结

| 检查项 | 结果 |
|---|---|
| 导演限制 | 5/5 守住 |
| 收场合规 | ✅ |
| 伏笔落地 | 2/2 有拍支撑 |
| 隔离审计 | ✅ 无泄露 |

整体判断：场景演绎符合 brief 约束，隔离严谨，收束完整，伏笔落地真实。

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


VERDICT: pass
ATTEMPT: r1
REDO_BEATS: []
ISOLATION: ok
REPORT: reviews/sc-0001-03.scene-check.r1.md
# 连续性审核报告 · ch-0001 · r2（复审）

报告名：reviews/ch-0001.continuity.r2.md

## 复审范围

本次复审为**增量核销模式**：仅核销 r1 总编报告指出的地名错误修正，不全量重审。

## 核销项

### MAJOR-1：验状地名错误（青槐镇 → 碑亭镇）

**原问题**：r1 总编检出正文旧契房验状将限制离镇范围写为"青槐镇"，与全书设定、角色 origin、场景 brief 不一致。

**修订声明**（revision-brief）：
- drafts/ch-0001.md：青槐镇 → 碑亭镇
- transcripts/sc-0001-02.md：Beat 7 与 SCENE RESULT 同步修正
- transcripts/sc-0001-03.md：初始情境同步修正
- context_packs/sc-0001-03.shen-yan.md：硬约束同步修正
- memory/working/ch-0001.md：工作态同步修正
- relay/HANDOFF.md：最近历史同步修正

**核验结果**：

| 目标文件 | 检索"青槐" | 检索"碑亭镇" | 核销状态 |
|----------|-----------|-------------|----------|
| drafts/ch-0001.md | 0 匹配 ✓ | 验状段 L144 + 章尾场景 L236 ✓ | **已修复** |
| transcripts/sc-0001-02.md | 0 匹配 ✓ | 验状落地句存在 ✓ | **已修复** |
| transcripts/sc-0001-03.md | 0 匹配 ✓ | 初始情境约束句存在 ✓ | **已修复** |
| context_packs/sc-0001-03.shen-yan.md | 0 匹配 ✓ | 硬约束段存在 ✓ | **已修复** |
| memory/working/ch-0001.md | 0 匹配 ✓ | 工作态约束句存在 ✓ | **已修复** |
| relay/HANDOFF.md | 0 匹配 ✓ | 历史记录句存在 ✓ | **已修复** |

**接缝检查**：验状约束（"沈砚亦不得擅离碑亭镇"）现与 `world/geography.md` 登记名、`characters/shen-yan.md` origin、全部 scene brief 一致；无地理认知断裂。

**无新增问题**：修订范围限定为地名替换，未触及情节点、人物状态、时间线或伏笔链条。

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


## 摘要

VERDICT: pass
ATTEMPT: r2
ISSUES: []
SEAM_CHECK: 地名修正后，验状约束与世界观/角色档案/场景 brief 完全对齐，无断裂。
REPORT: reviews/ch-0001.continuity.r2.md


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


## 备注

1. 本次复审仅核销 r1 总编 MAJOR-1，r1 连续性报告的其他 pass 结论默认延续（无理由重判）。
2. 全文检索确认当前事实源中已无"青槐"残留，地名一致性修复到位。
3. 建议后续 prose 阶段保持"碑亭镇/beiting-zhen"为唯一规范地名，避免再次引入未登记地名。
# 总编终审报告 · ch-0001 · r2（复审）

**报告名**：`reviews/ch-0001.editorial.r2.md`  
**审核对象**：`drafts/ch-0001.md`（第一章《至贱命格》）· 地名修正后复审  
**前置**：`reviews/ch-0001.continuity.r2.md` 已 pass；`revision-brief` status=revise-fixed  
**复审模式**：仅核销 r1 MAJOR-1（青槐镇→碑亭镇），有限抽查修订是否引入新问题；**不全量重审**。r1 其余 pass 结论与 MINOR 建议默认延续。

---

## 复审范围

| 项 | 范围 |
|----|------|
| 必核销 | r1 MAJOR-1：验状地名「青槐镇」≠ 登记名「碑亭镇」 |
| 有限抽查 | 修订接缝（验状约束 ↔ 章内/章尾地理指称 ↔ 场记/工作态）；是否因替换引入新剧情或世界观断裂 |
| 不重审 | r1 已 pass 的战力、OOC、因果、伏笔策略、可读性主项；r1 MINOR 不作二次展开（除非修订连带恶化） |

---

## 1. r1 MAJOR 核销

### MAJOR-1：验状地名错误（青槐镇 → 碑亭镇）

**原问题（r1）**：旧契房验状写「沈砚亦不得擅离**青槐镇**」，与 `world/geography.md` 登记「碑亭镇/beiting-zhen」、角色 origin、全部 scene brief 冲突。

**修订声明（revision-brief）**：六处事实源同步替换；验证目标为当前事实源无「青槐」残留。

**核验结果**：

| 目标 | 正文/场记证据 | 判定 |
|------|---------------|------|
| `drafts/ch-0001.md` 验状段 | 「沈砚亦不得擅离**碑亭镇**」 | ✓ 已修复 |
| `drafts/ch-0001.md` 章尾柯九短切 | 「**碑亭镇**另一头的客栈里」 | ✓ 与登记名一致，且强化地理锚点 |
| `transcripts/sc-0001-02.md` Beat 7 / SCENE RESULT | 「不得擅离碑亭镇」 | ✓ 已修复 |
| `transcripts/sc-0001-03.md` 初始情境 | 「不得擅离碑亭镇」 | ✓ 已修复 |
| `memory/working/ch-0001.md` sc-0001-02 增量 | 「本人不得擅离碑亭镇」 | ✓ 已修复 |
| 当前事实源全文检索「青槐」 | 六处目标文件 0 匹配 | ✓ 无残留 |

**接缝判定**：验状「不得擅离碑亭镇」现为后续 timeline / memory 的合法正式约束凭据；与沉鳞洞天开篇主场景设定一致，读者地理认知不再断裂。

**REPEAT**：否（r1 首次检出，r2 已修对）。

**核销结论**：**CLOSED ✓**

---

## 2. 有限抽查（修订是否引入新问题）

### 2.1 世界观 / 地理一致性（修订相关）

| 检查点 | 判定 | 说明 |
|--------|------|------|
| 替换是否改动情节 | ✓ | 仅地名对齐，验状条款、三日复核、禁离镇约束语义不变 |
| 章内地理指称自洽 | ✓ | 旧契房在「镇子东头」、碑林、镇衙、客栈均属碑亭镇辖域，无第二套镇名 |
| 是否引入未登记地名 | ✓ | 未新增；「青槐」已从当前事实源清除 |

### 2.2 因果 / 约束链（验状接缝）

| 检查点 | 判定 | 说明 |
|--------|------|------|
| 白日验状 → 夜间沈砚自检 | ✓ | 沈砚回忆「三日内持旧契复核」，与验状一致；禁离镇约束可支撑 ch-0002 窗口 |
| 场记 ↔ 正文 | ✓ | sc-0001-02 Beat 7、sc-0001-03 初始情境与正文验状句一致 |

### 2.3 修订附带变化（非 r1 要求，但不构成新问题）

正文旧契房段新增「**跑腿听熟的**」一句（沈砚回应三库分法），属对 r1 MINOR「旧契熟练度略巧」的**正向补强**，未越场记 BASIS，不属修订引入的 regress。

### 2.4 历史 artifact 说明（非本次拦稿项）

`relay/` 下旧 prompt/out、`reviews/sc-0001-02.scene-check.r1.md` 等归档仍含「青槐镇」——为 r1 前快照，**不在 revision-brief 当前事实源清单内**。发布链应以 `drafts/`、`transcripts/`、`memory/working/` 为准；若后续做仓库 hygiene，可择机同步历史 review，**不阻塞本章 editorial pass**。

---

## 3. r1 结论延续（不重审，仅确认修订未推翻）

| r1 维度 | r1 结论 | r2 复审 |
|---------|---------|---------|
| 世界观铁则（除地名外） | pass | 延续；地名项已关闭 |
| 战力 | pass | 延续 |
| OOC | pass | 延续 |
| 因果逻辑 | pass | 延续 |
| 伏笔策略 | pass | 延续 |
| 网文可读性 | pass（青槐损害信任） | 地名硬伤已除；r1 其余弱项仍为 MINOR 建议 |

---

## 4. 问题清单

### BLOCKERS

无。

### MAJOR

无（r1 MAJOR-1 已核销）。

### MINOR

延续 r1，修订未恶化；供二稿或发布前择机处理，**不拦 pass**：

1. **沈砚旧契熟练度略巧** — 正文已加「跑腿听熟的」，较 r1 略改善；若仍觉巧，可再补半句亲历（非必须）。
2. **柯九章尾「这个少年，有意思了」略俗** — 仍在；可换更贴 voice 的掂量句，可改可留。
3. **旧契房程序段信息密度** — 仍在；二稿提速时可压缩翻卷过程。
4. **记忆库 L2 patch 待办** — `memory/foreshadowing.md`、threads、章级 timeline 等发布前流程项；非正文 editorial 拦稿，但 Showrunner 发布前应完成。

---

## 5. 裁决说明

r1 唯一 MAJOR（验状青槐镇笔误）已在当前事实源**修对且无痕**；连续性 r2 已 pass；有限抽查未发现替换引入的新世界观断裂、因果断裂或剧情偏移。r1 其余判断力项未被本次修订推翻。

**本章 editorial 闸门：通过。** 可进入记忆更新与发布前流程（L2 memory patch 仍属 Showrunner 待办，非本章正文 revise）。

---

```
VERDICT: pass
ATTEMPT: r2
RETURN_TO: —
BLOCKERS: []
MAJOR: []
MINOR: [沈砚旧契熟练度略巧（已部分补强「跑腿听熟的」）；柯九章尾「有意思了」略俗；旧契房程序段略密可择机压缩；记忆库 L2 patch 待发布流程完成]
REPORT: reviews/ch-0001.editorial.r2.md
```
# 记忆回读校验 · ch-0001 · r1

REPORT: reviews/ch-0001.memory-verify.r1.md

## 依据
- memory/patches/ch-0001.patch.md
- memory/events.md
- memory/character-state.md
- memory/relationships.md
- memory/foreshadowing.md
- memory/threads.md
- memory/timeline.md

## 校验结果

VERDICT: verified

### 事件
- evt-0001: present once; known_by includes shen-yan / ke-jiu / 镇差 / 围观镇民.
- evt-0002: present once; known_by includes shen-yan / ke-jiu / 镇差 / 老账房.
- evt-0003: present once; known_by only shen-yan; secret=true.
- evt-0004: present once; known_by only ke-jiu; secret=true.

### 状态与关系
- shen-yan: inventory includes 拓纸、旧契凭据、三日复核验状；arc_progress set to 三日复核期·旧砚/拓纸异常待查.
- ke-jiu: inventory includes 隐秘笔记；arc_progress set to 三日复核窗口深查中.
- relationships: shen-yan→镇差, shen-yan→ke-jiu, ke-jiu→shen-yan all present once.

### 伏笔与线索
- fs-0001: open; ch-0001 清册压迫已追加.
- fs-0002: open; ch-0001 旧砚/拓纸异常已追加.
- thread-0002: open; 三日复核窗口.
- thread-0003: open; 拓纸残缺凹痕.

### 时间线
- evt-0001 through evt-0004 present once in timeline.

## 隔离说明
- 沈砚未获得 evt-0004（柯九建档/深查计划）。
- 柯九未获得 evt-0003（沈砚夜间亲见旧砚微温、拓纸自变、残缺反痕）。

created_by: showrunner@codex via codex-main · ch-0001-memory-verify.r1


## 正文和 memory 摘要


沈砚把呼吸放慢，闭了一会儿眼，又睁开。他记住拓纸凹痕所在的位置和三处断口的形状，在心里默念了两遍，然后不再想它。

明日先从旧契房的旧例里找说法。若能遇见守碑老人，就只旁敲侧击，不把纸和砚一并露出来。不急，一步一步来。


同一夜，碑亭镇另一头的客栈里，柯九正坐在灯下，面前摊着一本薄薄的笔记。

他手里拈着笔，笔尖悬在纸面上方，好一会儿没有落下。屋外更夫敲过二更，梆子声在夜风里传得很远。

他写下一行字：

“沈砚，碑林拓碑七年，随身旧砚，熟旧契房规矩。至贱命格——但命格这事，上头说过，不能只看面上判的。”

又写一行：

“旧具随工交接，经手栏空白。三日复核窗口可用。”

搁下笔，他把笔记合上，收入袖中暗袋。

窗外的月光照进来，在他脸上落下一道不深不浅的影。柯九吹熄了灯，在黑暗里坐了一会儿，然后低声自语了一句，声音轻得只有自己能听见：

“这个少年，有意思了。”


<!-- meta
next_hook: 沈砚需要在三日内持唯一线索——那方连他自己也说不清来历的旧砚——去镇衙复核。同一夜，柯九已经把“沈砚”写进另一份清单，而那份清单通向的，绝不是旧契房三库的分类法。
word_count: 3215
beats_covered: [sc-0001-01:b1-b6, sc-0001-02:b1-b7, sc-0001-03:b1-b6]
-->

# 已发生事件库（events）

> 仅记忆管理员可写（经 memory_patch）。`known_by` 是信息隔离的关键：
> 编认知包时，只有 `known_by` 里的角色能拿到该事件。版本 1 ·《碑外问道》。

| id | when | where | what | participants | known_by | secret |
|---|---|---|---|---|---|---|
| evt-mingge-secret | 多年前（正文前） | 司命/幽冥 | 沈砚命格被封局者借司命**改判镇压**为「至贱」，以掩其碑灵之锚身份 | 封局者(未现身)、司命体系 | 封局者(未现身)、司命体系 | true |
| evt-kejiu-mission | 开封前夜 | beiting-zhen | 柯九受"上头"指派，乔装游方修士潜入碑亭镇，探碑林开封并暗查「命格被动过手脚之人」 | ke-jiu、上头(未现身) | ke-jiu、上头(未现身) | true |
| evt-0001 | 封元 0 日午后 | beiting-zhen 碑林边 | 清册复核点名，镇差当众宣读沈砚「至贱命格」判词并要求交出旧砚入册查验；沈砚拒交并追问押印与归还章程 | shen-yan、镇差、ke-jiu | shen-yan、镇差、ke-jiu、围观镇民 | false |
| evt-0002 | 封元 0 日午后 | beiting-zhen 镇衙旧契房 | 沈砚以旧契房乙库程序反压镇差，老账房验状判定旧砚暂归沈砚照管、三日内复核、复核前不得离身外借、沈砚不得擅离碑亭镇 | shen-yan、镇差、ke-jiu、老账房 | shen-yan、镇差、ke-jiu、老账房 | false |
| evt-0003 | 封元 0 日夜 | beiting-zhen 碑林边破屋 | 沈砚独处时发现旧砚微温、拓纸自变、碑林方向极轻石响、拓纸右下角残缺凹痕与铅灰细迹；决定旧砚与拓纸分藏，暂不向镇差或柯九暴露异常 | shen-yan | shen-yan | true |
| evt-0004 | 封元 0 日夜 | beiting-zhen 客栈 | 柯九独处时将沈砚、旧砚、七年拓碑、经手簿空白栏记入隐秘笔记，将沈砚列为重点观察对象，拟借三日复核窗口深查 | ke-jiu | ke-jiu | true |

> ⚠️ 信息隔离落地：
> - `evt-mingge-secret` 的 `known_by` **不含 shen-yan**——给沈砚编认知包时永远取不到（对照其 must_not_know）。
> - `evt-kejiu-mission` 的 `known_by` **只含 ke-jiu/上头**——沈砚、苏决都不知道柯九的真实来意。

<!-- 正文中发生的事件从这里追加 -->
# 角色当前状态（character-state）

> 仅记忆管理员可写。随每章 patch 滚动更新。版本 1 ·《碑外问道》。

## shen-yan（沈砚）
- 修为：凡俗（未入修行）｜命格判词（明面）：至贱
- 情绪：戒备·守静｜位置：beiting-zhen（碑亭镇）·碑林边破屋｜伤势：健康
- inventory：[草鞋, 磕角旧砚, 拓纸(压入旧纸堆分藏), 旧契凭据, 三日复核验状]｜弧线进度：三日复核期·旧砚/拓纸异常待查
- 最近出现：ch-0001

## su-jue（苏决）
- 修为：ningang（凝罡·剑修，持本命飞剑）｜势力：jianyuan（斩荒剑垣）
- 情绪：冷峭、警觉｜位置：循线赶往碑亭镇一带（开篇尚未抵镇）｜伤势：健康
- inventory：[本命飞剑（未公开名）]｜弧线进度：离垣查线
- 最近出现：—

## ke-jiu（柯九 / 乔装"柯先生"）
- 修为：kaifu（开府，刻意压隐）｜势力：受雇于"上头"（待揭）
- 情绪：表面和气·内里高度戒备｜位置：beiting-zhen（碑亭镇）·客栈｜伤势：健康
- inventory：[游方修士行头（伪装）, 隐秘笔记(沈砚/旧砚/经手簿空白)]｜弧线进度：三日复核窗口深查中
- 最近出现：ch-0001
# 关系图（relationships）

> 仅记忆管理员可写。**有向边** a→b：a 对 b 的态度（b 不一定对等回应，需各记一条）。版本 1 ·《碑外问道》。

| 边 a→b | 信任(-10..10) | 性质 | 缘由 | 起始 |
|---|---|---|---|---|
| shen-yan→守碑老人(待建档) | +4 | 敬·亲近 | 镇口瞎眼老人偶尔照看、只言点拨 | 开篇 |
| shen-yan→镇差 | -6 | 抗拒·戒备 | 清册当众羞辱、夺砚未果但保留三日复核威胁 | ch-0001 |
| shen-yan→ke-jiu | -3 | 提防·疑 | 白日看似帮腔实则句句追旧砚来路，已视为需额外提防的外乡人 | ch-0001 |
| ke-jiu→shen-yan | 0 | 兴趣·观察 | 至贱命格但熟旧契房规矩、旧砚来历不明，列为重点观察对象 | ch-0001 |

> 其余关系待女主/反派等 `/character-create` 建档后补全（届时把"待建档"替换为其 slug）。
# 伏笔库（foreshadowing）

> 仅记忆管理员可写。总编每章核对：该回收的回收了吗？新埋的登记了吗？有无被遗忘的线。版本 1 ·《碑外问道》。

| id | 埋于 | 内容 | 隐显 | 状态 | 拟回收 | 已回收于 |
|---|---|---|---|---|---|---|
| fs-0001 | 开篇 | 沈砚命格被判「至贱」，处处透着不合常理（实为被镇压）；ch-0001 中被清册当众用作压迫依据，柯九注意到面上判词未必可信 | 隐晦 | open | 揭示命格改判真相（`evt-mingge-secret`） | — |
| fs-0002 | 开篇 | 那方磕角旧砚 / 无字碑林，遇异常时有微妙感应；ch-0001 中旧砚微温、拓纸自变、碑林极轻石响、拓纸残缺反痕与铅灰细迹落地，旧砚与拓纸已分藏 | 隐晦 | open | 揭示碑魂·本命字「拙」·碑灵之锚 | — |

> 状态：open（已埋未收）/ paid（已回收）/ abandoned（弃用）。
# 未决线索（threads）

> 仅记忆管理员可写。与伏笔区分：伏笔是"埋了等回收的暗示"；线索是"已摆上台面、尚未了结的冲突/任务/疑问"。版本 1 ·《碑外问道》。

| id | 开启于 | 内容 | 赌注 | 状态 | 关闭于 |
|---|---|---|---|---|---|
| thread-0001 | 开篇 | 沉鳞洞天封印将开，其封局真意与开封后气运归属未明 | 牵动各方势力，碑亭镇成棋盘 | open | — |
| thread-0002 | ch-0001 | 沈砚三日内须持旧砚至镇衙复核，复核结果未定；柯九拟借复核窗口深查经手簿与乙库残卷 | 旧砚是否被扣、沈砚是否继续被清册/镇规压住、柯九是否逼近真相 | open | — |
| thread-0003 | ch-0001 | 拓纸右下角残缺凹痕与铅灰细迹含义不明，沈砚决定明日从旧契房旧例与守碑老人侧查 | 旧砚/拓纸/无字碑林的关联是否暴露，沈砚是否更深卷入开封之局 | open | — |

> 状态：open / closed。
# 正文内时间轴（timeline）

> 仅记忆管理员可写。只记**开篇之后、正文中**发生的事（世界背景史在 `world/history.md`）。
> 连续性检查器据此校验事件先后、季节、年龄、时长。版本 1 ·《碑外问道》。

| id | t（可排序时间） | 章节 | 标签 |
|---|---|---|---|
| evt-0001 | 封元 0 日午后 | ch-0001 | 清册点名·碑林边 |
| evt-0002 | 封元 0 日午后 | ch-0001 | 旧契房验砚 |
| evt-0003 | 封元 0 日夜 | ch-0001 | 沈砚夜察异常 |
| evt-0004 | 封元 0 日夜 | ch-0001 | 柯九建档 |

> t 用自定历法即可，例如以"开封之日"为第 0 日，记作「封元 N 日」。
> 注：`evt-mingge-secret` 发生于正文前，属背景，不入本正文时间轴。
