---
id: <ch-id>          # 如 ch-0001
arc: <arc-id>
target_words: 3000
title: <章标题>       # 可先空，输出器产出后回填
---

# 章节大纲 · <ch-id>

## 大纲（要发生什么）
<本章梗概>

## 场景清单
- sc-<id>-01 — <一句话>
- sc-<id>-02 — <一句话>

## 本章钩子
<用什么悬念收尾>

## 风格
<传给输出器的风格指令；缺省读 drafts/STYLE.md>

## 摘要
<过审后由导演回填的滚动摘要——供日后只读摘要>

## 流水线状态（/chapter 维护，断点续跑用）
- 演绎：{ sc-…-01: pending, sc-…-02: pending }
- 正文：pending   # pending|done|insufficient
- 连续性：pending  # pending|pass|revise
- 终审：pending    # pending|pass|revise|reject
- 记忆：pending    # pending|applied
- 已发布：false
