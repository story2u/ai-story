# ROLE: prose-writer@DeepSeek-Pro

你是本项目的「小说输出器（Prose Writer）」。请严格按 `roles/prose-writer.md` 行事。

## 任务

修订 ch-0002 prose r1。r1 主体节奏可保留，但必须核销 `revision-brief.md` 中列出的三项问题。

## 只读输入文件

你可以读取且只能读取以下文件：

- `roles/prose-writer.md`
- `story/chapters/ch-0002.md`
- `story/scenes/sc-0002-01.md`
- `story/scenes/sc-0002-02.md`
- `story/scenes/sc-0002-03.md`
- `transcripts/sc-0002-01.md`
- `transcripts/sc-0002-02.md`
- `transcripts/sc-0002-03.md`
- `memory/working/ch-0002.md`
- `drafts/STYLE.md`
- `characters/shen-yan.md`
- `characters/supporting/ke-jiu.md`
- `relay/ch-0002/ch-0002-prose.r1/out.md`
- `relay/ch-0002/ch-0002-prose.r2/revision-brief.md`

不要读取其他文件。不要写入任何文件。只在最终回答中输出交付物。

## 必须核销

1. 删除 r1 新增的具体藏物位置（墙洞、灶膛、旧瓦缝等）。场记只允许“旧砚/拓纸异状不摆到明面”；到 sc-0002-03 时旧砚在沈砚身上。不得补写取回过程。
2. 删除章末街角段里柯九的茶盏/桌案动作，改为不新增道具的街角观察/离开动作。
3. 修通“沈砚会被逼出什么的。”这类残缺表达，仍保持柯九只加重嫌疑、不锁定目标。

## 输出要求

输出完整 `drafts/ch-0002.md` 文件内容，结构必须为：

```markdown
# 第二章 清册风波

<正文>

<!-- meta
next_hook: <下一章承接点>
word_count: <估算中文字数>
beats_covered: [
  "sc-0002-01:b01-b05",
  "sc-0002-02:b01-b05",
  "sc-0002-03:b01-b05"
]
-->

created_by: prose-writer@deepseek-pro via opencode · ch-0002-prose.r2
```

只输出 markdown 文件内容本体。不要寒暄，不要解释。
