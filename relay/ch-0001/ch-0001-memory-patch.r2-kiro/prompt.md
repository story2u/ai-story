# 任务：生成 ch-0001 memory patch（patch-ready，不应用）

你是记忆管理员。只输出 markdown；不要写文件，不要执行命令。报告目标 memory/patches/ch-0001.patch.md。
只依据当前黄金版 ch-0001。不要引用 v1。必须保护信息隔离：沈砚不知道柯九任务/建档；柯九不知道沈砚夜间异象细节。

## 输出格式

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


## 当前 memory

# 已发生事件库（events）

> 仅记忆管理员可写（经 memory_patch）。`known_by` 是信息隔离的关键：
> 编认知包时，只有 `known_by` 里的角色能拿到该事件。版本 1 ·《碑外问道》。

| id | when | where | what | participants | known_by | secret |
|---|---|---|---|---|---|---|
| evt-mingge-secret | 多年前（正文前） | 司命/幽冥 | 沈砚命格被封局者借司命**改判镇压**为「至贱」，以掩其碑灵之锚身份 | 封局者(未现身)、司命体系 | 封局者(未现身)、司命体系 | true |
| evt-kejiu-mission | 开封前夜 | beiting-zhen | 柯九受"上头"指派，乔装游方修士潜入碑亭镇，探碑林开封并暗查「命格被动过手脚之人」 | ke-jiu、上头(未现身) | ke-jiu、上头(未现身) | true |

> ⚠️ 信息隔离落地：
> - `evt-mingge-secret` 的 `known_by` **不含 shen-yan**——给沈砚编认知包时永远取不到（对照其 must_not_know）。
> - `evt-kejiu-mission` 的 `known_by` **只含 ke-jiu/上头**——沈砚、苏决都不知道柯九的真实来意。

<!-- 正文中发生的事件从这里追加 -->
# 角色当前状态（character-state）

> 仅记忆管理员可写。随每章 patch 滚动更新。版本 1 ·《碑外问道》。

## shen-yan（沈砚）
- 修为：凡俗（未入修行）｜命格判词（明面）：至贱
- 情绪：守静、戒备｜位置：beiting-zhen（碑亭镇）｜伤势：健康
- inventory：[草鞋, 磕角旧砚]｜弧线进度：开封前夜·启程前
- 最近出现：（开写后填章节）

## su-jue（苏决）
- 修为：ningang（凝罡·剑修，持本命飞剑）｜势力：jianyuan（斩荒剑垣）
- 情绪：冷峭、警觉｜位置：循线赶往碑亭镇一带（开篇尚未抵镇）｜伤势：健康
- inventory：[本命飞剑（未公开名）]｜弧线进度：离垣查线
- 最近出现：—

## ke-jiu（柯九 / 乔装"柯先生"）
- 修为：kaifu（开府，刻意压隐）｜势力：受雇于"上头"（待揭）
- 情绪：佯作和气、内里戒备｜位置：beiting-zhen（已潜入）｜伤势：健康
- inventory：[游方修士行头（伪装）]｜弧线进度：潜入探查中
- 最近出现：—
# 关系图（relationships）

> 仅记忆管理员可写。**有向边** a→b：a 对 b 的态度（b 不一定对等回应，需各记一条）。版本 1 ·《碑外问道》。

| 边 a→b | 信任(-10..10) | 性质 | 缘由 | 起始 |
|---|---|---|---|---|
| shen-yan→守碑老人(待建档) | +4 | 敬·亲近 | 镇口瞎眼老人偶尔照看、只言点拨 | 开篇 |

> 其余关系待女主/反派等 `/character-create` 建档后补全（届时把"待建档"替换为其 slug）。
# 伏笔库（foreshadowing）

> 仅记忆管理员可写。总编每章核对：该回收的回收了吗？新埋的登记了吗？有无被遗忘的线。版本 1 ·《碑外问道》。

| id | 埋于 | 内容 | 隐显 | 状态 | 拟回收 | 已回收于 |
|---|---|---|---|---|---|---|
| fs-0001 | 开篇 | 沈砚命格被判「至贱」，处处透着不合常理（实为被镇压） | 隐晦 | open | 揭示命格改判真相（`evt-mingge-secret`） | — |
| fs-0002 | 开篇 | 那方磕角旧砚 / 无字碑林，遇异常时有微妙感应 | 隐晦 | open | 揭示碑魂·本命字「拙」·碑灵之锚 | — |

> 状态：open（已埋未收）/ paid（已回收）/ abandoned（弃用）。
# 未决线索（threads）

> 仅记忆管理员可写。与伏笔区分：伏笔是"埋了等回收的暗示"；线索是"已摆上台面、尚未了结的冲突/任务/疑问"。版本 1 ·《碑外问道》。

| id | 开启于 | 内容 | 赌注 | 状态 | 关闭于 |
|---|---|---|---|---|---|
| thread-0001 | 开篇 | 沉鳞洞天封印将开，其封局真意与开封后气运归属未明 | 牵动各方势力，碑亭镇成棋盘 | open | — |

> 状态：open / closed。
# 正文内时间轴（timeline）

> 仅记忆管理员可写。只记**开篇之后、正文中**发生的事（世界背景史在 `world/history.md`）。
> 连续性检查器据此校验事件先后、季节、年龄、时长。版本 1 ·《碑外问道》。

| id | t（可排序时间） | 章节 | 标签 |
|---|---|---|---|
| _（示例，开写后替换）_ evt-0001 | 封元 0 日 | ch-0001 | 开封前夜·碑亭镇 |

> t 用自定历法即可，例如以"开封之日"为第 0 日，记作「封元 N 日」。
> 注：`evt-mingge-secret` 发生于正文前，属背景，不入本正文时间轴。


## 章内工作态

# 章内工作态 · ch-0001

## sc-0001-01 清册点名
- source: `transcripts/sc-0001-01.md` / `reviews/sc-0001-01.scene-check.r1.md`
- status: scene-pass

### 角色状态增量
- shen-yan: 未交出旧砚；被镇差从碑林边逼往镇衙旧契房验明清册旧规；对镇差抗拒加深；对柯九起提防。
- ke-jiu: 确认沈砚值得继续盯；重点记下沈砚、旧砚、七年拓碑三条线；对沈砚兴趣升级，并视旧砚为值得追查之物。

### 关系/认知增量
- 沈砚与镇差: 清册压力未解除，但当场夺砚暂缓；冲突转入镇衙旧契房验规矩。
- 沈砚与柯九: 柯九公开插话试探；沈砚对柯九起提防。
- 柯九与旧砚线索: 旧砚被柯九盯上，但仍未显异。

### 伏笔/线索触及
- fs-0001: 至贱命格被当众作为压迫依据。
- fs-0002: 旧砚被盯上但不显异。

created_by: memory-manager@ollama via ollama · sc-0001-01-working-memory.r1 (Showrunner cleaned terminal control chars and removed unregistered fs-0003)

## sc-0001-02 旧契占理
- source: `transcripts/sc-0001-02.md` / `reviews/sc-0001-02.scene-check.r1.md`
- status: scene-pass

### 角色状态增量
- shen-yan: 凭旧契房程序逼镇差退半步，旧砚暂归他照管；三日内须持旧契至镇衙复核，复核前旧砚不得离身、不得外借，本人不得擅离碑亭镇；对柯九反复试探更警惕。
- ke-jiu: 确认沈砚、旧契、旧砚三条线都值得深查；将经手簿、乙库残卷和“旧具随工交接”记为可查线索；对沈砚兴趣再升级。

### 关系/认知增量
- 沈砚与镇差: 镇差当场夺砚失败，但保留清册复核威胁；冲突从“当场夺砚”转入“三日复核期”。
- 沈砚与柯九: 柯九继续以和气闲谈旁敲侧击；沈砚已把柯九视为需要额外提防的外乡人。
- 柯九与旧砚/旧契: 旧具来历仍不闭环，“随工交接”成为柯九后续可追的程序缺口。
- 沈砚与旧契房程序: 沈砚熟悉旧契房流程这一能力面外显，能用凡俗旧规为自己争一线余地。

### 伏笔/线索触及
- fs-0001: 清册与旧契之间不合常理的缝隙被进一步坐实；经手簿与乙库残卷给出可查入口，但旧具来历仍未闭环。
- fs-0002: 旧砚暂留沈砚手中，物件连续性保住；旧砚仍未显异。

created_by: memory-manager@ollama/minimax-m3 via ollama · sc-0001-02-working-memory.r1 (Showrunner removed future-event wording)

## sc-0001-03 夜半反痕
- source: `transcripts/sc-0001-03.md` / `reviews/sc-0001-03.scene-check.r1.md`
- status: scene-pass

### 角色状态增量
- shen-yan: 进门落闩确认无人跟后，将旧砚旧布裹紧贴身收好，拓纸与旧契凭据逐张理平折齐压在手边；疲惫加深但未崩。油灯挪测、触摸窗缝墙根桌面排查后，判定拓纸变暗不似灯影或屋内潮气；把拓纸从“白日凭据”提升为需单独看管的异常物；对旧砚与拓纸之间是否有关联产生疑心。拓纸按折痕单独压入不起眼的旧纸中，与旧契凭据、旧砚皆分开；吹低灯芯守夜。对白日风波的判断从“镇差欺压旧事”转为“旧砚与拓纸都被牵连”；自我约束从“忍住”转为“按规矩逐步应对”；决定明日侧查旧契旧例、碑林旧例，并谨慎旁敲守碑老人。
- ke-jiu: 独处暗处低声自语，翻动随身笔记本将白日所得线索速记于隐秘卷轴；将沈砚列为重点观察对象；决定在三日复核窗口内先查经手簿与乙库残卷，再进旧契房继续追踪；情绪表面和气、内里高度戒备。

### 关系/认知增量
- 沈砚与镇差/柯九: 白日风波未落地，戒备继续加深；沈砚意图守住旧砚、拓纸与旧契凭据不被旁人借题拿走，暂不向镇差或柯九透露拓纸与旧砚的异常。
- 沈砚与旧砚: 旧砚仍贴身裹紧，不再与拓纸同放；对旧砚与拓纸之间是否有关联起疑但未下定论。
- 沈砚与拓纸: 拓纸不再只是“白日凭据”，已上升为需单独看管的异常物；右下角有非寻常墨拓的凹痕（深浅不一、中间断开三处）与铅灰色细迹，含义不明，不可贸然示人。
- 沈砚与碑林方向: 拓纸自变与碑林方向极轻石响先后相接，沈砚判断“可能有关、也可能只是巧合”，未贸然外推。
- 柯九与沈砚/旧砚/旧契/经手簿/乙库残卷: 白日线索整理完毕，建档为待查线索；拟借三日复核窗口继续深查。
- 柯九与剑垣/山水衙门: 明确不惊动，修为不外露；仍不能确认沈砚就是上头要找的命格异人。

### 伏笔/线索触及
- fs-0002: 旧砚微温、拓纸自变（纸色变暗、纸角无风自卷）、碑林方向极轻石响、拓纸右下角残缺凹痕与铅灰细迹落地；旧砚与拓纸已分藏，物件连续性保住。
- fs-0001: 清册压迫与旧契复核压力继续外推；沈砚对白日风波的判断从“镇差欺压旧事”转为“旧砚与拓纸都被牵连”；柯九三日复核窗口调查线并入章尾钩子。

created_by: memory-manager@ollama/minimax-m3 via ollama · sc-0001-03-working-memory.r1 (Showrunner cleaned terminal control chars and wrapped lines)


## 正文 meta 与摘要信息

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


## 场景结果

transcripts/sc-0001-01.md:67:## SCENE RESULT
transcripts/sc-0001-01.md-68-outcome: 沈砚没有交出旧砚，但被镇差从碑林边逼往镇衙旧契房验明清册旧规；柯九确认沈砚值得继续盯，重点记下沈砚、旧砚、七年拓碑三条线。
transcripts/sc-0001-01.md-69-emotional_beats: [当众羞辱压场, 沈砚以规矩护砚, 柯九闲话试探, 镇差退成旧契房验规矩]
transcripts/sc-0001-01.md-70-proposed_deltas: [沈砚对镇差抗拒加深且对柯九起提防, 柯九对沈砚兴趣升级并视旧砚为值得追查之物, 清册压力未解除但夺砚暂缓]
transcripts/sc-0001-01.md-71-foreshadow_touched: [fs-0001 至贱命格被当众作为压迫依据, fs-0002 旧砚被盯上但未显异]
transcripts/sc-0001-01.md-72-isolation_self_check: 演员 prompt 仅递公开 SPEAK/ACT 与各自认知包；未向任何演员暴露他人 INNER、旧砚真相、柯九真实身份或不在场信息。B1.5 r1 因引用未提供的"上一回开封"信息作废，r2 已纠正。
transcripts/sc-0001-01.md-73-
transcripts/sc-0001-01.md-74-created_by: showrunner@claude via cowork-main · sc-0001-01-transcript-init
--
transcripts/sc-0001-03.md:66:## SCENE RESULT
transcripts/sc-0001-03.md-67-outcome: 沈砚独处时发现旧砚微温与拓纸残缺反痕，但无法解释，只把拓纸与旧砚分开藏好并意识到白日风波没有结束；柯九在别处把沈砚列为重点观察对象，准备借三日复核窗口深查。
transcripts/sc-0001-03.md-68-emotional_beats: 沈砚从强压疲惫转入细查异常，再由不安转为按规矩守物、明日侧查旧例；柯九从表面闲散转为暗中建档、谨慎深查。
transcripts/sc-0001-03.md-69-proposed_deltas: 沈砚掌握拓纸变暗、纸角自卷、残缺凹痕与铅灰细迹；沈砚决定旧砚与拓纸分藏，暂不向镇差/柯九暴露异常；柯九把沈砚列为重点观察对象，拟查经手簿、乙库残卷与旧契房线索。
transcripts/sc-0001-03.md-70-foreshadow_touched: fs-0002 旧砚/拓纸/无字碑林微弱感应落地；fs-0001 清册压迫与旧契复核压力继续外推；柯九三日复核窗口调查线并入章尾钩子。
transcripts/sc-0001-03.md-71-isolation_self_check: 沈砚未获得柯九暗中建档、开府修为或上头任务信息；柯九未获得沈砚夜间亲见的旧砚微温、拓纸自变、残缺反痕细节。
transcripts/sc-0001-03.md-72-
transcripts/sc-0001-03.md-73-created_by: showrunner@codex via codex-main · sc-0001-03-transcript-init
--
transcripts/sc-0001-02.md:73:## SCENE RESULT
transcripts/sc-0001-02.md-74-outcome: 沈砚以旧契房程序逼镇差退半步，旧砚暂归他照管，但三日内须持旧契复核，复核前旧砚不得离身、不得外借，沈砚也不得擅离碑亭镇；柯九确认沈砚与旧契、旧砚都有可查价值。
transcripts/sc-0001-02.md-75-emotional_beats: [旧契房程序反压镇差, 经手簿与乙库残卷给出可查线索, 旧具来历仍不闭环, 旧砚暂留但复核压力加身, 柯九把沈砚与旧砚记成深查对象]
transcripts/sc-0001-02.md-76-proposed_deltas: [沈砚保住旧砚但被三日复核与禁擅离镇压住, 沈砚对柯九试探更警惕, 柯九对沈砚兴趣加深并确认旧砚线索值得追, 镇差当场夺砚失败但保留清册复核威胁]
transcripts/sc-0001-02.md-77-foreshadow_touched: [fs-0001 清册与旧契之间存在不合常理的缝隙, fs-0002 旧砚被保住并将带回夜间异痕]
transcripts/sc-0001-02.md-78-isolation_self_check: 演员 prompt 仅递公开 SPEAK/ACT/WORLD_BEAT 与各自认知包；未向任何演员暴露他人 INNER、旧砚真相、命格改判真相、碑魂或不在场信息。B2.5/B2.7 为世界拍，B2.6 柯九 prompt 未包含沈砚 INNER。
transcripts/sc-0001-02.md-79-
transcripts/sc-0001-02.md-80-created_by: showrunner@codex via codex-main · sc-0001-02-transcript-init


## 审核结论

连续性 r2 pass；总编 r2 pass。
