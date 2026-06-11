# AI 编剧室 · 模型无关的多 Agent 小说创作 Harness

像「虚拟剧组」一样写长篇网文：世界观架构师立法、导演排戏、**角色演员各演各的（无上帝视角）**、
总编终审、记忆管理员落库、输出器把演完的戏写成正文。

**它不是软件，是一套文档 + 协议。** 角色定义是可粘进任意大模型的 markdown「角色卡」；
你给每个角色**指定一个模型**（GPT / Claude / DeepSeek …），由总控按 `playbook/0-cli-relay.md` **调度本机
CLI 自动接力**（`claude -p` / `codex exec` / `opencode run`），汇成小说；没有 CLI 的模型可人肉粘贴降级。

## 它的形态

- ❌ 不是"让一个 AI 直接写小说"，也不是要你写代码去跑。
- ✅ 是 **角色卡（`roles/`）+ 接力协议（`playbook/`）+ 文档化世界与记忆（`world/ memory/ …`）**。
- ✅ 模型无关：换模型只改 `cast.md`，人设与连续性都在文档里，不会丢。

## 三条最重要的原则

1. **信息隔离靠构造**：给某角色开的是一个干净对话，里面只粘它该知道的四样东西——秘密你压根不递，它就演不出破绽。
2. **文件系统是唯一事实源**：对话会丢会满，一切先落盘成 markdown 再继续。
3. **闸门制**：连续性 + 总编任一不过即回退，每章必落库记忆，绝不带病发布。

## 怎么开始

1. 读 **`HARNESS.md`**（操作宪法）、**`cast.md`**（角色→CLI 选角）和 **`playbook/0-cli-relay.md`**（调度协议）。
2. 按 `playbook/` 逐步做：
   - `playbook/1-world-create.md` —— 把世界观架构师卡粘进模型，产出 `world/`
   - `playbook/2-character-create.md` —— 建角色（每个必须有"认知边界"）
   - `playbook/3-arc-design.md` —— 产出弧线 / 章纲 / 场景清单
   - `playbook/4-scene-run.md` —— **场景演绎**：在各角色窗口间接力（系统最核心的动作），收尾跑**场景验收**
   - `playbook/5-prose-generate.md` —— 把场记写成正文
   - `playbook/6-review-commit.md` —— 机械核对 + 总编 + 记忆落库（带回读校验）+ 提交
   - `playbook/7-arc-retro.md` —— **弧线回顾**：伏笔/线索债务盘点 + 把审稿教训硬化为规则
   - `playbook/chapter-pipeline.md` —— 串起整章（含循环账本与回退预算，见 `HARNESS.md §10` 循环宪法）
3. 推荐 Claude Code 当总控（Showrunner）：它组 prompt、调度三个 CLI 轮动、校验落盘、跑闸门——
   **主会话自己不演任何角色**。便捷命令：`/world-create` `/scene-run` `/chapter` 等。

## 目录速览

```
HARNESS.md      操作宪法（先读这个）
AGENTS.md       任意 agent（Codex/DeepSeek/…）接入说明；Claude 系另见 CLAUDE.md
cast.md         选角表：角色 → 模型
roles/          7 张职能/角色卡 + showrunner 总控卡（可粘进任意模型）
playbook/       接力工作流（0=CLI 调度协议；1–7=各阶段把什么给谁、输出存哪）
relay/          调度留痕（每次 dispatch 的 prompt 与原始输出，I 组审计凭证）
templates/      markdown 模板：角色 / 场景 brief / 认知包 / 记忆补丁 / 修订指令(revision-brief)
checklists/     发布前自检清单（替代代码校验）
world/          世界观（markdown，仅架构师写）
characters/     角色档案（含认知边界，演员只读）
story/          arcs / chapters / scenes（仅导演写）
context_packs/  私有认知包（仅记忆管理员写）—— 信息隔离的载体
transcripts/    场景原始演绎记录
drafts/         正文 + STYLE.md（仅输出器写）
reviews/        审核报告
memory/         长期记忆（markdown + 轻量结构，仅记忆管理员写）
```

> 建议 `git init`：每章一次提交，记忆随章落库，可回滚到任意时刻的世界状态。
