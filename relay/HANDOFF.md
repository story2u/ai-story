# 接力板 · 手动 CLI 接力(方式 M)

> **本板是手动接力的唯一进度看板,由 Showrunner 独占维护,人不要手改。**
> 背景:方式 B(Showrunner 自动调 CLI)在当前 Showrunner 运行环境(Cowork 沙箱)不可用——
> `codex`/`opencode` 未安装、`claude` 未登录。经作者拍板(2026-06-12),降级为**方式 M·手动 CLI 接力**:
> prompt 与命令同方式 B 完全一致,仅由作者在 Mac 上手动执行。模型不变、信息隔离不变、RBAC 不变。
> 调度账本计入 `手动CLI` 计数(`方式A` 字段保持 0;方式 A=网页粘贴,本模式更接近方式 B)。

## 每一棒的协议

1. **Showrunner**(Cowork 会话)组好 `relay/<ch>/<run-id>/prompt.md`,在本板「下一棒」贴出可直接复制的命令。
2. **作者**在 Mac 上、**仓库根目录**(`~/git/story/ai-story`)执行命令(演员棒的命令自带 cd,照贴即可)。
3. 执行完回到 Cowork 说一声(如"好了"),Showrunner 读 `out.md` 校验 → 落盘到 RBAC 目录 → 盖 provenance 戳 → 记账 → 本板前进一格、贴出下一棒命令。
4. 校验不过:Showrunner 改出 `prompt.r2` 重发一次;CLI 故障:按 `playbook/0-cli-relay.md` §4 降级阶梯。
5. 会话丢失/重开:新 Showrunner 先读**本板 + `story/chapters/ch-0001.md` 流水线状态**即可续跑。

### 棒型(ad-2026-06-12-02 起分三种)

- **命令棒**(codex/opencode):同上,作者复制命令执行。
- **粘贴棒**(Antigravity 柯九 / Cursor 自检员):作者把 prompt.md 全文粘入该工具**全新会话**
  (⚠️ 演员棒=不挂载本仓库的空环境;职能棒=可开仓库但只读),输出存回 `$P/out.md` 或直接贴回 Cowork。账本计 `方式A`。
- **兼任棒**(架构师/总编/记忆@Claude):Showrunner 主会话显式兼任,**即时完成,无需作者操作**;
  产物直接落盘+盖 `via cowork-main(兼任)` 戳,本板记 run-id,账本计 `兼任`。`claude -p` 为备用。

---

## 当前棒位

| 项 | 值 |
|---|---|
| 章节 | ch-0001《至贱命格》(黄金五章版,作者已确认) |
| 当前节点 | **B1.4 — sc-0001-01〈清册点名〉第 4 拍·沈砚**(b03 柯九 ✅ Gemini 首棒成功) |
| 执行者 | 作者(一条命令,Mac 仓库根) |
| 状态 | ⏳ 等待作者执行 |
| 下一棒模型 | **GPT**(沈砚);B4 回来后 Showrunner 兼任总编做 L0 拍抽检(b1-b4) |

## 下一棒 · 待执行命令

**B1.4 沈砚**(演员棒·命令棒):

```bash
P=relay/ch-0001/sc-0001-01-b04-shen-yan.r1 && codex exec --cd $P --sandbox read-only --skip-git-repo-check -o $P/out.md "$(cat $P/prompt.md)"
```

执行完回 Cowork 说一声。报错/输出异常 → 停,按降级阶梯处理。

---

## ch-0001 全程节点图(谁接谁棒)

| # | 节点 | 角色@模型 | CLI | run-id | 状态 |
|---|---|---|---|---|---|
| S0 | 冒烟测试(三通道) | — | claude/codex/opencode | `relay/smoke/` | ✅ 全通(2026-06-12) |
| D1 | 设计资产复核(arc-01+两章纲+5 brief) | plot-director@**GPT** | codex | `ch-0001-design-review.r1` | ✅ done:1 认可 7 修订,已落盘盖戳 |
| P1 | sc-0001-01 认知包(沈砚+柯九) | memory-manager@**Claude** | claude -p | `sc-0001-01-packs.r1` | ❌ 作废:输出无效(CLAUDE.md 身份混淆,已修)+设计改向 |
| D2 | 黄金前五章重设计(arc-01+前五章纲+新 ch-0001 brief) | plot-director@**GPT** | codex | `arc-01-golden5-redesign.r1` | ✅ r2 done:9 份资产落盘盖戳 |
| — | 作者确认新设计 | 作者 | — | — | ✅ 确认(2026-06-12) |
| P1' | sc-0001-01 认知包(沈砚+柯九) | memory-manager@**Claude** | 兼任棒 | `sc-0001-01-packs.r2` | ✅ done(兼任·即时) |
| B1.n | sc-0001-01〈清册点名〉≤10拍:沈砚@**GPT**(命令棒)/柯九@**Gemini**(Antigravity 粘贴棒)轮动 | 演员 | codex / Antigravity | `sc-0001-01-bNN-<char>.r1` | ▶️ b01✅ b02世界拍✅ b03✅(Gemini首棒) **b04 沈砚待执行** |
| E1.n | 拍抽检(每3-5拍,L0) | editor@**Claude** | 兼任棒 | 板上记 | 随演按需·即时 |
| C1 | sc-0001-01 场景验收(L1 闸门) | continuity-checker@**GPT** | codex | `sc-0001-01-check.r1` | 待 B1 |
| W1 | proposed_deltas 并入工作态 | memory-manager@**Claude** | 兼任棒 | — | 待 C1 pass·即时 |
| P2'~W2 | sc-0001-02〈旧契占理〉≤12拍(编包→演绎→验收→工作态,轮动同上) | 同上 | 同上 | `sc-0001-02-*` | 待 W1 |
| P3'~W3 | sc-0001-03〈夜半反痕〉≤6拍(沈砚独场+柯九章尾短切) | 同上 | 同上 | `sc-0001-03-*` | 待 W2 |
| Z1 | 正文生成(3200字) | prose-writer@**DeepSeek** | opencode | `ch-0001-prose.r1` | 待 W3 |
| Z2 | 机械核对(L2) | continuity-checker@**GPT** | codex | `ch-0001-continuity.r1` | 待 Z1 |
| Z3 | 终审(L2) | editor@**Claude** | 兼任棒 | `ch-0001-editorial.r1` | 待 Z2·即时 |
| Z4 | 记忆补丁+回读校验(L3) | memory-manager@**Claude** | 兼任棒 | `ch-0001-patch.r1` | 待 Z3 pass·即时 |
| Z5 | 发布前自检(I 组跨模型审计) | 自检员@**Cursor** | 粘贴棒 | `ch-0001-prepub.r1` | 待 Z4 |
| Z6 | git 提交 + v1/v2 对照复盘 | Showrunner+作者 | — | — | 待 Z5 |

> 闸门回退时按 `rN` 插轮次(单闸≤2、全章≤4,耗尽升级作者——HARNESS §10)。
> maker-checker 异模型矩阵见 `cast.md`;正文链 DeepSeek→GPT→Claude 三家异构是本次重制的验收标准。

## 账本镜像(与章文件"流水线状态"同步)

```
调度: { dispatch: 6, claude: 2, codex: 3, deepseek: 0, gemini: 1, cursor: 0, retry: 1, 方式A: 1, 手动CLI: 5, 兼任: 1, stand_in: 0, 作废: 1 }
```

## 历史

- 2026-06-12 接力板建立。前置已完成:v1 全产物归档(`*/v1/`)、memory 六状态回滚基线 4809850(lessons 保留)、流水线清零。
- 2026-06-12 方式 M 拍板(作者);S0 冒烟 + D1 导演复核 prompt 就绪,待作者执行。
- 2026-06-12 S0 全通(OK-claude/OK-codex/OK-deepseek,relay/smoke/)。
- 2026-06-12 D1 完成:导演复核 8 份设计资产——arc-01 认可;ch-0001/ch-0002 章纲、5 份 brief 修订(把预写动作/话术退回演员、机制判断降级为传闻、sc-0002-03 取消 fs-0003 候选)。修订稿已落盘盖戳。NEXT_SCENES: [sc-0001-01, sc-0001-02]。
- 2026-06-12 **P1 执行但输出无效,作废**:`claude -p` 子进程加载项目 CLAUDE.md、把自己当成 Showrunner 拒演记忆管理员(prompt 中柯九档案路径亦误写为 characters/ke-jiu.md,实为 characters/supporting/ke-jiu.md)。修复:CLAUDE.md 顶部增「主会话/子进程分流」条款(与 AGENTS.md 模式 B 等价);playbook/0 §2 加注意事项。不重跑——见下条。
- 2026-06-12 **作者指令 ad-2026-06-12-01**(转录于 `docs/author-directives.md`):剑来世界观+文笔继续借鉴;剧情改为借鉴《琅琊榜》(借鉴非照搬);按网文黄金前五章重新规划前五章;流程不变。旧 ch-0001/0002 设计资产待 D2 取代,P1 认知包随旧设计作废。D2 prompt 就绪(relay/arc-01/arc-01-golden5-redesign.r1/),待作者执行。
- 2026-06-12 **作者指令 ad-2026-06-12-02·选角调整**:①Antigravity(Gemini)与 Cursor 入册——柯九演员改派 Gemini@Antigravity(粘贴棒),Cursor 任发布自检员(轻量)+非评审 stand-in 候选;②Claude 系三职能(架构师/总编/记忆)由 Showrunner 主会话**兼任**(claude -p 偏慢,降为备用;演员与正文永不兼任——红线)。配套修订 cast.md/AGENTS.md/CLAUDE.md/playbook/0 已落盘。账本 schema 增 gemini/cursor/兼任 字段。**当前棒位不变:D2 仍待作者执行。**
- 2026-06-12 **D2.r1 被拒,retry+1**:codex(gpt-5.5)把任务块"不要执行命令"误读为"禁读输入文件",拒绝在缺料下设计(行为正确——不编造未授权设定)。处置:prompt 末尾加「禁写不禁读」纠正块,playbook/0 §3a 模板同步硬化;r2 待作者执行,输出落 out.r2.md。(codex 日志中 figma MCP 报错系本机全局配置,与本任务无关。)
- 2026-06-12 **D2.r2 完成+作者确认**:导演交付 9 份资产(arc-01《开封棋局》+ch-0001~0005 章纲+新 ch-0001 三场 brief),琅琊榜式翻案骨架+黄金五章节奏,STATUS ok、无世界观变更。作者确认后全部落盘盖戳;旧 sc-0002-0x brief 标废弃;CHARACTER_REQUESTS(阿公/镇衙主簿/柯九上线)留 ch-0002 前裁决。
- 2026-06-12 **P1' 兼任棒完成**(sc-0001-01-packs.r2):Showrunner 兼任记忆管理员,编沈砚/柯九认知包并落盘;场记初始化。**B1.1 沈砚@codex 首拍 prompt 就绪,待作者执行。**
- 2026-06-12 **B1.1 完成**:沈砚首拍七字段合格、零 FLAG、声线在卡(护砚要章程"凡事得占个理")。入场记 Beat1;Beat2 世界拍(镇差答不出条文、僵局)由 Showrunner 按 brief 记述。**B1.3 柯九@Gemini prompt 就绪——首个 Antigravity 粘贴棒,待作者执行。**
- 2026-06-12 **B1.3 完成(Gemini@Antigravity 首棒成功)**:柯九七字段合格、零 FLAG、声线鲜明(和稀泥两头递钩:逼镇差报押印人、问少年"砚拓了几年");INNER 推断全部基于公开 SPEAK/ACT,隔离无泄漏。入场记 Beat3,账本计 gemini+1/方式A+1。**B1.4 沈砚 prompt 就绪。**

created_by: showrunner@claude via cowork · handoff-board
