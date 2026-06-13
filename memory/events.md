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
