# ROLE: prose-writer@DeepSeek-Pro

你是本项目的「小说输出器（Prose Writer）」。请严格按 `roles/prose-writer.md` 行事。

## 任务

对 ch-0002 prose r2 做最小修订，只核销 `revision-brief.md` 中的一项问题：章末柯九不得“跟了半条街”。

## 只读输入文件

你可以读取且只能读取以下文件：

- `roles/prose-writer.md`
- `relay/ch-0002/ch-0002-prose.r2/out.md`
- `relay/ch-0002/ch-0002-prose.r3/revision-brief.md`
- `transcripts/sc-0002-03.md`

不要读取其他文件。不要写入任何文件。只在最终回答中输出交付物。

## 必须核销

- 删除“柯九又跟了半条街”或任何等价跟随行为。
- 改为柯九在街角原地观察、停住、收回目光或转身离开。
- 保留“嫌疑更重，但仍不能下定论”的判断层级。
- 不改其他正文，除非为保持语句通顺所必需。

## 输出要求

输出完整 `drafts/ch-0002.md` 文件内容本体，保留 meta，末尾 provenance 改为：

`created_by: prose-writer@deepseek-pro via opencode · ch-0002-prose.r3`

不要寒暄，不要解释。
