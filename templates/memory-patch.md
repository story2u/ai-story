# 记忆补丁 · <ch-id>

> 由记忆管理员在章节过审后产出，写入 `memory/patches/<ch-id>.patch.md`。
> 声明式、**幂等**（用稳定 id 去重，重复应用不产生重复条目）。Showrunner 审阅后，逐条应用到 `memory/*.md`。

- **依据**：transcripts/<sc>.md … ｜ drafts/<ch-id>.md

## 事件入库 → memory/events.md（每条标 known_by，控制下章信息隔离）
- `evt-XXXX`｜when:<时间锚>｜where:<地点>｜what:<一句话>｜participants:[..]｜**known_by:[..]**｜secret:true/false

## 角色状态 → memory/character-state.md
- `<char-id>`：set { realm:.. mood:.. location:.. hp:.. arc_progress:.. }｜inventory +[..] -[..]

## 关系 → memory/relationships.md（有向边）
- `<a>-><b>`：set { trust:<-10..10> sentiment:<爱/恨/敬/惧/愧> note:.. }

## 伏笔 → memory/foreshadowing.md
- `fs-XXXX`：op=plant|payoff|revise｜detail:..｜status→ open|paid|abandoned

## 未决线索 → memory/threads.md
- `thread-XXXX`：op=open|close|revise｜detail:..

## 时间线 → memory/timeline.md
- `evt-XXXX`：t:<可排序时间>｜label:..

---
**摘要（给 Showrunner 审阅）**：<本补丁人话摘要>
