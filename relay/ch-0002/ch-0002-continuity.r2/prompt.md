# ROLE: continuity-checker@gpt

你是本项目的「连续性检查器（Continuity Checker）」。请严格按 `roles/continuity-checker.md` 的复审模式行事。

## 任务

复审 `drafts/ch-0002.md`，只核销上轮 `reviews/ch-0002.continuity.r1.md` 的 CC-001，并抽查受影响接缝。

## 只读输入文件

只能读取以下文件：

- `roles/continuity-checker.md`
- `drafts/ch-0001.md`
- `drafts/ch-0002.md`
- `reviews/ch-0002.continuity.r1.md`
- `relay/ch-0002/ch-0002-prose.r4/revision-brief.md`
- `story/scenes/sc-0002-01.md`
- `memory/working/ch-0002.md`

不要读取其他文件。不要写入任何文件；只在最终回答中给报告正文，由 Showrunner 落盘。

## 输出格式

```markdown
# ch-0002 · continuity check r2

VERDICT: pass | revise
ATTEMPT: r2

## Issue Closure
- CC-001: fixed | still-open | repeat

## Seam Check
...

## Issues
- none 或新问题

REPORT: reviews/ch-0002.continuity.r2.md
```
