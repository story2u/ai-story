# 发布前自检报告 · ch-0001 · r1

**报告名**：`reviews/ch-0001.pre-publish.r1.md`  
**章节**：ch-0001《至贱命格》  
**自检员**：发布自检员 @ Cursor Agent  
**模式**：只评不改 · 对照 `checklists/pre-publish.md` A–I  
**前置闸门**：连续性 pass(r2) · 总编 pass(r2) · 记忆 verified(r1)

---

## 总览

| 组 | 判定 | 摘要 |
|---|---|---|
| A 信息隔离审计 | **pass** | 三场验收 + memory-verify 均确认隔离；作废拍已清 |
| B 连续性 | **pass** | 对照 continuity r2；当前事实源无「青槐」残留 |
| C 设定与战力 | **pass** | editorial r2 延续 r1 pass；无铁则/战力越级 |
| D 人物与逻辑 | **pass** | 关键转折有动机；OOC 无拦稿项 |
| E 伏笔与线索 | **pass** | fs-0001/fs-0002、thread-0002/0003 已落库 |
| F 正文边界 | **pass** | 正文覆盖声明 beats；prose r2 已修场记越界项 |
| G 记忆与归档 | **pass** | patch 已应用并 verified；working 已删；摘要已回填 |
| H 循环卫生 | **pass** | 场景验收齐全；章级回退有 brief；轮次 1/4 未超预算 |
| I 跨模型痕迹审计 | **fail** | 主链异模型成立，但关键产物 provenance 戳不完整 |

---

## A. 信息隔离审计

| 检查项 | 判定 | 证据 |
|---|---|---|
| 认知包无越权秘密 | **pass** | `context_packs/sc-0001-*.md` 均设「此刻不知」盲区；sc-0001-02 packs r1/r2 作废后 r3 落盘 |
| 演绎未串包/INNER | **pass** | 三场 scene-check ISOLATION: ok；B5「上一回开封」r1 作废 |
| 独立干净会话 | **pass** | 各 run 在 `relay/ch-0001/` 有独立 prompt/out |
| `known_by` 正确 | **pass** | `memory-verify.r1`：evt-0003 仅 shen-yan；evt-0004 仅 ke-jiu |

**结论：pass**

---

## B. 连续性

| 检查项 | 判定 | 证据 |
|---|---|---|
| 章首衔接 | **pass** | 第一章，开篇自洽（continuity r1） |
| 道具/状态一致 | **pass** | 旧砚链条完整；`character-state.md` 与正文一致 |
| 地理/时间线 | **pass** | 封元 0 日午后→夜；验状已统一「碑亭镇」 |
| 称谓/离场者 | **pass** | 苏决未乱入；镇差为 NPC 称谓 |

**结论：pass**（r2 已核销青槐镇笔误）

---

## C. 设定与战力

| 检查项 | 判定 | 证据 |
|---|---|---|
| 无违 `world/rules.md` | **pass** | 全章无越阶斗法；异象极轻 |
| 战力压制合理 | **pass** | editorial r1/r2：无战斗、无越级 |
| 规则变更已批准 | **pass** | 无架构师级规则变更 |

**结论：pass**

---

## D. 人物与逻辑

| 检查项 | 判定 | 证据 |
|---|---|---|
| 无 OOC | **pass** | 沈砚守规矩抗辩、柯九旁敲侧击均贴人设 |
| 转折有铺垫 | **pass** | 旧契房程序、七日拓碑、经手簿空白均有铺垫 |

**结论：pass**

---

## E. 伏笔与线索

| 检查项 | 判定 | 证据 |
|---|---|---|
| 该回收已回收 | **pass** | 本章为开篇埋设，无待回收项 |
| 新埋已登记 | **pass** | `foreshadowing.md` fs-0001/fs-0002 已更新 |
| 线索已更新 | **pass** | `threads.md` thread-0002/0003 已开启 |

**结论：pass**

---

## F. 正文边界

| 检查项 | 判定 | 证据 |
|---|---|---|
| 正文未越权创作 | **pass** | prose r2 修掉「赵四」私名、旧砚位置链、七日→三日；`beats_covered` 与三场场记对齐 |

**结论：pass**

---

## G. 记忆与归档

| 检查项 | 判定 | 证据 |
|---|---|---|
| patch 已审阅并 verified | **pass** | `reviews/ch-0001.memory-verify.r1.md` VERDICT: verified |
| working 已删 | **pass** | `memory/working/` 无 ch-0001 文件 |
| 摘要已回填 | **pass** | `story/chapters/ch-0001.md` 摘要段完整 |
| 写权限合规 | **pass** | 各产物通道与 `cast.md` 大体一致（详见 I 组例外） |

**结论：pass**

---

## H. 循环卫生（重点）

| 检查项 | 判定 | 证据 |
|---|---|---|
| 每场景验收 pass | **pass** | `reviews/sc-0001-01/02/03.scene-check.r1.md` 均 pass |
| 回退有 revision-brief | **pass** | `ch-0001-prose.r2/revision-brief.md`；`ch-0001-editorial.r2/revision-brief.md`；`ch-0001-continuity.r2/revision-brief.md`；拍级作废见 HANDOFF/场记 inline |
| 轮次未超预算 | **pass** | 回退累计 **1/4**（prose r1→r2 + editorial r1→r2 地名修正） |
| 审报按轮次归档 | **pass** | continuity/editorial 均有 r1/r2；`lessons.md` ls-0001/ls-0002 已 hardened |
| 演员未收审稿/lessons | **pass** | 抽查 prompt 仅含角色卡+认知包+公开场记+本拍指令 |

**H 组观察（不拦 pass）**：
- `reviews/sc-0001-02.scene-check.r1.md` 归档快照仍写「青槐镇」——revision-brief 已声明为 r1 前 artifact，当前事实源已修
- `ls-0003`（认知包「碑上的字早已看惯」）仍为 **open·次数 1**，未达 REPEAT 硬化阈值

**结论：pass**

---

## I. 跨模型痕迹审计（重点）

### I.1 provenance 戳对照

| 产物 | 要求 maker@模型 | 实际 | 判定 |
|---|---|---|---|
| 章纲 `story/chapters/ch-0001.md` | plot-director@gpt | 有 `created_by` | ✓ |
| 场记各拍 `transcripts/sc-0001-*.md` | 演员/世界拍 | 每拍有 `created_by` | ✓ |
| 正文 `drafts/ch-0001.md` | prose-writer@deepseek | **文件内无 `created_by` 戳**；仅 `relay/ch-0001/ch-0001-prose.r2/` 留痕 | **✗** |
| 连续性审报 | continuity-checker@gpt | r1/r2 内容 pass，**reviews 文件无尾戳**；HANDOFF 记 r1 为 Kiro | △ |
| 总编审报 | editor@cursor | r2 pass，**reviews 文件无尾戳**；relay 有 run | △ |
| 认知包 | memory-manager@ollama | 六包均有 `created_by` | ✓ |
| 记忆 patch | memory-manager | **`memory/patches/ch-0001.patch.md` 无 `created_by`**；`relay/.../ch-0001-memory-patch.r2-kiro/` 有 run | **✗** |

### I.2 maker-checker 矩阵

| 链路 | 判定 | 说明 |
|---|---|---|
| 正文 DeepSeek → 连续性(Kiro/GPT) → 总编 Cursor | **pass** | 与 cast 矩阵一致，均异模型 |
| 场记演员 → 场景验收(GPT/Kiro/Ollama) | **pass** | sc-0001-01@GPT，02@Kiro，03@Ollama |
| 认知包 Ollama/DeepSeek → 验收隔离审计 | **pass** | 编入后由异模型 scene-check 审计 |
| L0 sc-0001-01 spotcheck | **warn** | `editor-spotcheck@deepseek` stand-in 抽检批次含 `stand-in-ke-jiu@deepseek` b05——L0 同模型；但 L1 由 GPT pass，主闸门未破 |

### I.3 调度账本

| 检查项 | 判定 | 证据 |
|---|---|---|
| 账本记入章文件 | **pass** | `story/chapters/ch-0001.md` 调度段完整 |
| stand_in 合规 | **warn** | 账本 `stand_in: 4`；B2.1 有「作者 DeepSeek 主创指令」；其余 3 次仅有 HANDOFF 叙述，**无独立「作者当场批准」签字记录** |
| 评审同模型 stand-in | **warn** | 见上 L0 b05 项；L1 已异模型覆盖 |
| 演员 prompt 抽查 ×2 | **pass** | `sc-0001-03-b01-shen-yan.r1/prompt.md`、`sc-0001-02-b06-ke-jiu.r1/prompt.md`：无仓库路径、无他人 INNER/认知包、无不在场拍 |

**prompt 归档注意**：`sc-0001-03-b01` relay prompt 快照仍含「青槐镇」，但正式认知包与场记/正文已改为「碑亭镇」——属 relay 归档滞后，**不影响当前事实源**，建议 hygiene 时同步。

### I.4 冻结通道使用

| 项 | 判定 |
|---|---|
| Claude 冻结期用于 sc-0001-01 认知包（兼任） | **warn** — 已标注 `memory-manager@claude via cowork-main(兼任)`，属历史通道，不拦内容但不符合当前 cast 默认编组 |
| Gemini 历史用于 sc-0001-01-b03 | **warn** — 已弃用，后续未再调度 |

**结论：fail**（关键产物 provenance 戳未写入正文事实源）

---

## 问题清单

### BLOCKERS

1. **I-001 · 正文缺少 provenance 戳**  
   `drafts/ch-0001.md` 无 `created_by: prose-writer@deepseek via opencode · ch-0001-prose.r2`（或等价戳）。清单 I 要求关键产物本体带戳，不能仅依赖 `relay/` 镜像。

2. **I-002 · 记忆 patch 缺少 provenance 戳**  
   `memory/patches/ch-0001.patch.md` 无 `created_by`（应为 `memory-manager@kiro via kiro-cli · ch-0001-memory-patch.r2-kiro` 或 Showrunner 应用戳）。

### WARNINGS

1. **I-W01 · stand_in=4 批准记录不完整** — 仅 B2.1 沈砚 stand-in 有明确作者指令；B1.5 柯九、P2 认知包、L0 spotcheck 缺独立批准条。
2. **I-W02 · L0 同模型抽检** — DeepSeek stand-in L0 覆盖 DeepSeek stand-in 产出的 b05；建议记入 lessons 或改派异模型 L0。
3. **I-W03 · 章级审报 reviews 文件缺尾戳** — `ch-0001.continuity.r1/r2.md`、`ch-0001.editorial.r2.md` 无 `created_by`。
4. **H-W01 · 归档 artifact 含旧地名** — `reviews/sc-0001-02.scene-check.r1.md` 等仍写「青槐镇」。
5. **H-W02 · ls-0003 仍 open** — 首次出现，观察中。
6. **流程-W01 · 过早标记已发布** — `story/chapters/ch-0001.md` 流水线状态 `已发布: true` 早于本次发布前自检完成。
7. **editorial MINOR 延续** — 柯九章尾「有意思了」略俗；旧契房程序段略密（不拦发布）。

---

## 按组判定汇总

```
A: pass
B: pass
C: pass
D: pass
E: pass
F: pass
G: pass
H: pass
I: fail
```

---

```
VERDICT: fail

BLOCKERS: [
  "I-001: drafts/ch-0001.md 缺少 created_by provenance 戳",
  "I-002: memory/patches/ch-0001.patch.md 缺少 created_by provenance 戳"
]

WARNINGS: [
  "I-W01: stand_in=4，仅部分有作者当场批准记录",
  "I-W02: sc-0001-01 L0 DeepSeek 抽检含 DeepSeek stand-in 产出 b05",
  "I-W03: 章级 reviews/*.md 缺 created_by 尾戳",
  "H-W01: 归档 scene-check 仍含已修正地名「青槐镇」",
  "H-W02: lessons ls-0003 仍 open",
  "流程-W01: 章文件已标记已发布:true 早于 pre-publish 完成",
  "editorial MINOR: 柯九章尾措辞、旧契房信息密度"
]

REPORT: reviews/ch-0001.pre-publish.r1.md
```

---

## 放行建议（供 Showrunner，非本角色执行）

1. 为 `drafts/ch-0001.md`、`memory/patches/ch-0001.patch.md` 补 `created_by` 戳后重跑 I 组抽查。  
2. 将 `story/chapters/ch-0001.md` 的 `已发布: true` 改回 false，待本报告 pass 后再 commit。  
3. 可选 hygiene：同步归档 review/relay 中的「青槐镇」旧快照；补 stand-in 批准记录或降账本计数说明。  

**内容闸门（A–H + 连续性/总编/记忆）已就绪；当前唯一硬拦项为 I 组 provenance 落盘不完整。**
