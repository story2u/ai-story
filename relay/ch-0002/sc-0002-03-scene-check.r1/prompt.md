# L1 场景验收 · sc-0002-03

你是连续性检查器，只评不改。本场含 GPT/Codex actor，因此使用 Kiro 异模型 checker。不要写文件，只输出报告正文。

## 验收目标
对 `sc-0002-03 · 禁令上墙` 做四项机械核对：
1. 导演限制逐条守住？
2. 收场是否命中 exit_condition，且 beat_budget 内合理？
3. 伏笔 plant/touch 是否有真实拍支撑？
4. 隔离审计是否 ok：沈砚没收到柯九 INNER/任务/上午碎片；柯九没收到沈砚 INNER/昨夜异常；认知包无泄漏。

## scene brief 摘要
- 必须是“禁令上墙”，不得写苏决登场或 ch-0003 内容。
- 禁令：“命格低劣、役籍不明者，不得夜近碑林”等限制公开上墙，沈砚名字列第一列。
- 沈砚意识到对方不是随手欺负，而是一步步把他从碑林边、旧契保护和熟悉地盘上剥离。
- 章末钩子：禁令落款印记与夜里拓纸暗痕极细相似。
- 不得解释命格真相、旧砚机制、拓纸暗痕含义。
- 不得让柯九锁定沈砚真实身份；只能嫌疑加重。
- 不得让沈砚当场撕令、毁令、夜闯碑林或正面破解禁令。

## 完整场记

```markdown
$(sed -n '1,320p' transcripts/sc-0002-03.md)
```

## 认知包摘要

### 沈砚
- 知昨日清册/旧契房/昨夜旧砚拓纸异常/sc-0002-01 阿公方向。
- 不知命格真相、旧砚机制、柯九真实身份/目的/记录、柯九上午旧档碎片。

### 柯九
- 知任务、昨日清册/旧契房、上午三块碎片，沈砚是最需压测嫌疑对象但未锁定。
- 不知沈砚昨夜异常、沈砚/阿公私谈、命格真相、旧砚机制。

## 输出格式
```
VERDICT: pass | redo
ATTEMPT: r1
REDO_BEATS: []
ISOLATION: ok | leak(证据)
REPORT: reviews/sc-0002-03.scene-check.r1.md

## Report Body
<可直接落盘的报告>
```

created_by: continuity-checker@kiro(stand-in-gpt due maker-checker separation) via kiro-cli · sc-0002-03-scene-check.r1
