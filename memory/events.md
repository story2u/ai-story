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
