# Playbook 0 · CLI 自动接力（运行方式 B · 调度协议）

> 解决的问题:运行方式 A(人肉粘贴)摩擦太大,实践中一切角色都被 Showrunner stand-in 代演,
> 多模型轮动名存实亡(ch-0001/0002 v1 的教训)。本协议把"接力"从人肉剪贴板升级为
> **Showrunner 用 Bash/粘贴通道调度多个模型**,真正轮动,且把"代演"通道焊死。
>
> 宪法地位:文档仍是唯一状态源与媒介(`HARNESS.md` 公理②)。本协议允许的自动化**仅限接力动作**:
> 调用另一个模型 CLI 或整理干净新会话粘贴接力,并把其输出落盘——仍然没有业务脚本,没有代码状态。

---

## 1. 一次调度(dispatch)= 一次接力

原"开某角色的干净窗口、粘四块、取回输出"在 B 模式下变为:

```
① 组 prompt   Showrunner 把该角色该看的内容写进 relay/<ch>/<run-id>/prompt.md
② 调用        按 cast.md 该角色那行的命令模板,Bash 调对应 CLI(非交互单次)
③ 收输出      模型原始输出存 relay/<ch>/<run-id>/out.md
④ 校验        结构对不对(七字段/verdict 字段/无寒暄无越权)?不对→重发一次
⑤ 落盘        Showrunner 把合格产物写进它该去的目录(RBAC),并盖 provenance 戳
```

**run-id 命名**:拍级 `sc-0003-01-b04-shen-yan.r1`;阶段级 `ch-0003-continuity.r1`、`ch-0003-prose.r1`。
`relay/` 整目录入 git——它就是旧协议里"会话窗口"的审计留痕。

**三条不变式**:
1. **被调度角色只输出文本,永不写文件。** 落盘永远由 Showrunner 做——RBAC(`HARNESS.md §3`)由单点执行。
2. **每次调度无状态、自包含。** CLI 单次调用不带会话记忆,所以每个 prompt 必须装齐该角色全部所需
   (角色卡全文+任务块)。角色的"连续性"来自文档(认知包/场记/memory),不来自会话——这反而是公理②的强化。
3. **Codex Showrunner 主会话不扮演角色。** 没有默认兼任;架构师/总编/记忆也走 `cast.md` 指定通道。
   Claude 保留主创候补身份但当前冻结,作者解除冻结前不调度、不 stand-in、不冒烟测试。

## 2. 命令模板(与 cast.md 配套)

设 `P=relay/<ch>/<run-id>`,先 `mkdir -p $P` 并写好 `$P/prompt.md`。

| 模型 | CLI | 职能角色(需读仓库) | 演员(禁读任何文件) |
|---|---|---|---|
| GPT | `/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex` | `/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex exec --sandbox read-only --output-last-message $P/out.md "$(cat $P/prompt.md)"` (cwd=仓库根) | `/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex exec --cd $P --sandbox read-only --skip-git-repo-check --output-last-message $P/out.md "$(cat $P/prompt.md)"` |
| DeepSeek | `opencode` | `opencode run -m deepseek/deepseek-chat "$(cat $P/prompt.md)" > $P/out.md` (cwd=仓库根) | `(cd $P && opencode run -m deepseek/deepseek-chat "$(cat prompt.md)" > out.md)` |
| Kiro | `kiro-cli` | `kiro-cli chat --no-interactive "$(cat $P/prompt.md)" > $P/out.md` (cwd=仓库根) | `(cd $P && kiro-cli chat --no-interactive "$(cat prompt.md)" > out.md)` |
| Antigravity | `agy` | `agy --model "GPT-OSS 120B (Medium)" -p "$(cat $P/prompt.md)" > $P/out.md` (cwd=仓库根) | `(cd $P && agy --model "GPT-OSS 120B (Medium)" -p "$(cat prompt.md)" > out.md)` |
| Cursor | Cursor / `cursor-agent` | 总编/发布自检员:Cursor 打开仓库**只读**粘贴任务,或 `cursor-agent -p`(以本机为准) | 演员候选,规则同 Antigravity 行 |
| Ollama | `ollama` | **当前弃用**:`kimi-k2.6:cloud` 实测返回 403 subscription required;账号权限恢复前不调度 | **当前弃用** |
| Claude | `claude` | **冻结不启用**;解除冻结后才可加回 `claude -p "$(cat $P/prompt.md)" > $P/out.md` | **冻结不启用** |

无 CLI 的粘贴棒:作者把 `$P/prompt.md` 全文粘入该工具**全新会话**,输出存回 `$P/out.md`(或贴回 Showrunner 落盘),账本计 `方式A`。

- 模型号以本机为准:`opencode models`、`/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex exec --help`、`kiro-cli chat --list-models`、`agy models`、`cursor-agent --help`;在 cast.md 改,此表不动。
- codex 的进度流走 stderr、最终消息走 stdout/`-o`,正好只取交付物。
- 所有 CLI 都按"单次调用"使用;**不要**用 resume/session 续聊(会引入会话态,破坏不变式 2)。
- Claude 冻结期任何 `claude -p` 调用都应视为误调度;若必须启用,先由作者解除冻结并同步 `cast.md` / `CLAUDE.md` / 接力板。

## 3. prompt 组装模板

### 3a. 职能角色(导演/总编/连续性/输出器/记忆/架构师——有上帝视角,可读仓库)

```
<roles/<角色>.md 全文>
---
# 本次任务(Showrunner 调度 · 非交互单次调用)
- 本条消息+下列输入文件 = 你的全部上下文;输出一次给全,无后续追问机会。
- 只输出交付物本体(markdown)。不要寒暄/复述任务;不要写任何文件、不要执行命令——落盘由 Showrunner 负责。
- ⚠️ 上一条的"禁"是**禁写不禁读**:下列输入文件**需要你主动读取**(read-only sandbox);
  禁止的是写/改文件、读清单之外的文件。(2026-06-12 硬化:D2 run 曾因此歧义被拒,见接力板历史)
- 输入文件(只读,按你角色卡的"输入"清单): <逐个列路径>
- 任务: <一句话,如"对 ch-0003 做机械核对(角色卡清单7项+追溯抽查)">
- 输出格式: <角色卡规定的格式:verdict 报告/正文+meta/patch/认知包…>
```

### 3b. 演员(character-actor——零上帝视角,prompt 即全部世界)

```
<roles/character-actor.md 全文>
---
# YOU ARE
<characters/<id>.md 人设要点,Showrunner 摘录>
# 你的私有认知包
<context_packs/<sc>.<id>.md 全文>
# 公开场记(只含你亲历的拍,已过可见性过滤,无任何 INNER)
<…>
# 本拍指令(导演)
<…>
# 输出要求
仅输出七字段:SPEAK/ACT/INNER/BASIS/STATE_DELTA/KNOWLEDGE_GAINED/FLAG。
你处于无状态单次调用:本条消息是你的全部世界。禁止读取任何文件、禁止使用任何工具。
```

**演员隔离的 B 模式落地**(`HARNESS.md §1①`"不递那张牌"):
- prompt 里**绝不出现仓库路径**;演员调用 cwd 锁在 `$P`(空目录),codex 加 read-only sandbox。
- 重演时演员只收"第 n 拍作废"声明+新本拍指令,照旧(§10 铁律1)。
- 行为兜底:场景验收的"隔离审计"会在场记里查不可能知识(角色说出了没递给它的信息=泄漏)。

## 4. 校验与降级阶梯

**④校验不过**(字段缺失/夹带闲话/输出器报 insufficient 之外的越权):同一 prompt 末尾加一行格式纠正,
重发 **1 次**(同 run-id,out.r2.md)。再不过 → 按降级阶梯走,并在流水线状态计 `retry+1`。

**降级阶梯**(CLI 报错/限额/反复格式不合时,逐级下落,每级落盘记录):
1. 重试 1 次(等额度/换 `-m` 同家备用模型,cast.md 备注列)。
2. **退回运行方式 A**:把 `$P/prompt.md` 原样交给用户,人肉贴到该模型的网页/App,贴回输出。模型没变,只是通道变了。
3. **stand-in(最后手段,需用户当场批准)**:换一个模型代演,产物标 `stand-in-<角色>(<代演模型>)`,
   流水线状态 `stand_in+1`。**红线:评审角色(总编/连续性/场景验收)绝不允许由"与被审产物 maker 同模型"者 stand-in
   ——宁可冻结本章等通道恢复。**(maker-checker 异模型是 v2 的底线,见 §10 铁律2)
4. 用户不在场 → 写断点进章文件"流水线状态",暂停流水线。

## 5. provenance 戳与调度账本(可审计的轮动)

- **每个落盘产物**末尾盖戳:`created_by: <角色>@<模型> via <cli> · <run-id>`
  (例:`created_by: prose-writer@deepseek via opencode · ch-0003-prose.r1`)。stand-in 时如实标注。
- **章文件"流水线状态"**新增一行调度账本:
  `调度: { dispatch: 23, codex: 8, deepseek: 6, kiro: 2, antigravity: 3, cursor: 2, claude: 0, retry: 2, 方式A: 3, stand_in: 0 }`
- 发布前过 `checklists/pre-publish.md` **I 组(跨模型痕迹审计)**:戳与 cast.md 一致、maker≠checker、
  stand_in=0(非 0 需作者签字)。

## 6. 通道冒烟测试(每章第一次启用某通道前)

给本章会用到的 CLI 各发一条 10 字以内的自报家门任务,确认通道可用再开演:
```bash
/Users/bruce/.nvm/versions/node/v24.13.0/bin/codex exec --sandbox read-only "回答:OK-codex"
opencode run -m deepseek/deepseek-chat "回答:OK-deepseek"
kiro-cli chat --no-interactive "回答:OK-kiro"
agy --model "GPT-OSS 120B (Medium)" -p "回答:OK-agy"
```
Cursor 等粘贴通道用全新会话粘一条 `回答:OK-<通道>` 做人工冒烟,输出记入 `relay/smoke/` 或接力板。
Ollama 当前不用;若作者恢复 `kimi-k2.6:cloud` 订阅权限,重测通过后再写回 cast/接力板。
Claude 不做默认冒烟;解除冻结前不测试、不调度。
任一必需通道不通 → 先修通道或按 §4 决定降级,不要带病开演。

---
> 各 playbook 里凡写"开 X 的窗口",在运行方式 B/M 下一律读作"按本协议调度 X"。
> 选角与命令参数见 `cast.md`;宪法依据见 `HARNESS.md §0/§1①/§10`。
