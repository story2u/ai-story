# 记忆补丁 · ch-0001

│ 由记忆管理员在章节过审后产出，写入 memory/patches/ch-0001.patch.md。
│ 声明式、**幂等**（用稳定 id 去重，重复应用不产生重复条目）。Showrunner 审阅后，逐条应用到 memory/*.md。

- **依据**：transcripts/sc-0001-01.md, sc-0001-02.md, sc-0001-03.md ｜ drafts/ch-0001.md

## 事件入库 → memory/events.md

| id | when | where | what | participants | known_by | secret |
|---|---|---|---|---|---|---|
| evt-0001 | 封元 0 日午后 | beiting-zhen 碑林边 | 清册复核点名，镇差当众宣读沈砚「至贱命格」判词并要求交出旧砚入册查验；沈砚拒交并追问押印与归还章程 | shen-yan, 镇差, ke-jiu | shen-yan, 镇差, ke-jiu, 围观镇民 | false |
| evt-0002 | 封元 0 日午后 | beiting-zhen 镇衙旧契房 | 沈砚以旧契房乙库程序反压镇差，老账房验状判定旧砚暂归沈砚照管、三日内复核、复核前不得离身外借、沈砚不得擅离碑亭镇 | shen-yan, 镇差, ke-jiu, 老账房 | shen-yan, 镇差, ke-jiu, 老账房 | false |
| evt-0003 | 封元 0 日夜 | beiting-zhen 碑林边破屋 | 沈砚独处时发现旧砚微温（自内向外）、拓纸自变（纸色变暗、纸角无风自卷）、碑林方向极轻石响、拓纸右下角残缺凹痕与铅灰细迹；决定旧砚与拓纸分藏，暂不向镇差或柯九暴露异常 | shen-yan | shen-yan | true |
| evt-0004 | 封元 0 日夜 | beiting-zhen 客栈 | 柯九独处时将沈砚、旧砚、七年拓碑、经手簿空白栏记入隐秘笔记，将沈砚列为重点观察对象，拟借三日复核窗口深查 | ke-jiu | ke-jiu | true |

## 角色状态 → memory/character-state.md

- shen-yan：set { mood: 戒备·守静, location: beiting-zhen 碑林边破屋, arc_progress: 三日复核期·旧砚/拓纸异常待查 } | inventory +[旧砚(贴身藏), 拓纸(压入旧纸堆分藏), 旧契凭据, 三日复核验状]
- ke-jiu：set { mood: 表面和气·内里高度戒备, location: beiting-zhen 客栈, arc_progress: 三日复核窗口深查中 } | inventory +[隐秘笔记(沈砚/旧砚/经手簿空白)]

## 关系 → memory/relationships.md

- shen-yan→镇差：set { trust: -6, sentiment: 恨, note: 清册当众羞辱、夺砚未果但保留三日复核威胁 }
- shen-yan→ke-jiu：set { trust: -2, sentiment: 惧, note: 白日看似帮腔实则句句追旧砚来路，已视为需额外提防的外乡人 }
- ke-jiu→shen-yan：set { trust: 0, sentiment: 兴趣, note: 至贱命格但熟旧契房规矩、旧砚来历不明，列为重点观察对象 }
- ke-jiu→旧砚：set { trust: 0, sentiment: 疑, note: 经手栏空白、来历不闭环、值得追查 }

## 伏笔 → memory/foreshadowing.md

- fs-0002：op=revise | detail: 旧砚微温（自内向外）、拓纸自变（纸色变暗、纸角无风自卷）、碑林方向极轻石响、拓纸右下角残缺凹痕与铅灰细迹均已落地；旧砚与拓纸已分藏 | status→ open
- fs-0003：op=plant | detail: 经手簿「旧具随工交接」栏空白，来历不闭环 | status→ open | 拟回收：揭示旧砚真正来历与碑灵之锚关联

## 未决线索 → memory/threads.md

- thread-0002：op=open | detail: 沈砚三日内须持旧砚至镇衙复核，复核结果未定；柯九拟借复核窗口深查经手簿与乙库残卷
- thread-0003：op=open | detail: 拓纸右下角残缺凹痕与铅灰细迹含义不明，沈砚决定明日从旧契房旧例与守碑老人侧查

## 时间线 → memory/timeline.md

- evt-0001：t: 封元 0 日午后 | label: 清册点名·碑林边
- evt-0002：t: 封元 0 日午后 | label: 旧契房验砚
- evt-0003：t: 封元 0 日夜 | label: 沈砚夜察异常
- evt-0004：t: 封元 0 日夜 | label: 柯九建档

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


摘要（给 Showrunner 审阅）：本章入库四条事件（两条公开、两条秘密），更新沈砚与柯九状态，新增四条有向关系边，推进 fs-0002（旧砚/拓纸异常落地）、新埋 fs-0003（经手簿空白），开启两条未决线索（三日复核、拓纸凹痕）。信息隔离已保护：沈砚不知柯九任务/建档；柯九不知沈砚夜间亲见的旧砚微温、拓纸自变、残缺凹痕细节。
