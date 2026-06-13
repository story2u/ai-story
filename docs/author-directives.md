# 作者指令记录（authorial directives · Showrunner 转录归档）

> 作者的创作方向裁决高于一切设计资产。每条指令由 Showrunner 如实转录，
> 据此调度导演/架构师修订设计；执行情况记在接力板（`relay/HANDOFF.md`）与各章流水线状态。

## ad-2026-06-12-01 · 剧情改向：借鉴《琅琊榜》+ 网文黄金前五章（v2 创作基调）

作者原话要点（2026-06-12，方式 M 会话）：

1. 世界观架构参考《剑来》没有错——**剑来的世界观和文笔都可以继续借鉴**；
2. 但剑来的剧情过于拖沓、写到后面烂尾——**剧情不学剑来**；
3. **这部小说的剧情要借鉴《琅琊榜》**——是借鉴，不是完全照搬；
4. 按**网文"黄金前五章"的阅读习惯**，重新思考并规划本书前五章；
5. v2 版本即按黄金前五章的模式来创作；
6. 现行创作流程（方式 M 接力 / 闸门 / RBAC / 主会话不代演）没有问题，继续保持。

Showrunner 执行记录：

- 调度 plot-director@gpt 重设计 arc-01 开篇骨架 + 前五章章纲 + 新 ch-0001 场景 brief
  （run: `arc-01-golden5-redesign.r1`）。
- 此前 D1（`ch-0001-design-review.r1`）复核过的 ch-0001/ch-0002 章纲与 5 份 brief，自本指令起**待重设计取代**；
  `docs/remake-v2-plan.md` 的"两章重制"范围扩展为"前五章按黄金五章规划、逐章产出"
  （其方式 M 运行方式、验收标准、v1 归档处置不变）。
- P1（`sc-0001-01-packs.r1`）认知包随旧设计作废（该 run 本身亦因 CLAUDE.md 身份混淆输出无效，见接力板历史）。
- 导演重设计产物回来后，**先交作者确认，再恢复演绎流水线**。

created_by: showrunner@claude via cowork（转录作者指令） · ad-2026-06-12-01

## ad-2026-06-12-02 · 选角与通道调整：Antigravity/Cursor 入册，Claude 职能由主会话兼任

作者原话要点（2026-06-12，方式 M 会话）：

1. 更新 AGENTS.md，让 **Antigravity** 和 **Cursor** 也参与到项目中，分配的角色可以**轻量一点**；
2. 目前 claude code（`claude -p` 通道）响应偏慢，**由 Showrunner（Cowork 主会话）代替 claude code 的角色**。

Showrunner 执行记录与边界裁定：

- **主会话兼任范围 = 三个 Claude 系职能角色**：世界观架构师、总编、记忆管理员。
  兼任规则：切换为该角色卡行事、按其输出格式产出、产物盖 `via cowork-main(兼任)` 戳、账本计 `兼任`；
  `claude -p` 降为备用通道。总编兼任失去"异会话独立性"（cast.md 原注的底线），系作者知情权衡，
  I 组审计中如实标注；终审仍只审 DeepSeek 正文与 GPT 结构，无自产自审。
- **红线（不在兼任范围）**：演员**柯九**。主会话持全局上帝视角，而演员必须零上帝视角——
  主会话兼任演员=摧毁信息隔离（v1 教训的核心）。柯九改派 **Gemini@Antigravity**，
  三家演员仍全异模型（沈砚@GPT / 苏决@DeepSeek / 柯九@Gemini）。
- **新通道轻量角色**：
  - Antigravity（Gemini）：演员·柯九（每拍一小段，干净新会话粘贴；本机若有 `gemini` CLI 可走 CLI）。
  - Cursor（模型以本机配置为准）：发布前自检员（`checklists/pre-publish.md` 机械审计，
    含 I 组跨模型痕迹审计——由独立第四通道核查最可信）；兼任降级阶梯的非评审 stand-in 候选池。
- 配套修订：cast.md（选角与矩阵）、AGENTS.md（IDE 型 agent 接入规则）、CLAUDE.md（铁规例外条款）、
  playbook/0（不变式 3 修订、命令模板补行）、relay/HANDOFF.md（接力协议更新）。

created_by: showrunner@claude via cowork（转录作者指令） · ad-2026-06-12-02
