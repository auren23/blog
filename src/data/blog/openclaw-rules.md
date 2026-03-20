---
author: Xeron
pubDatetime: 2026-03-17T00:00:00Z
title: 我给 OpenClaw 立的规矩
slug: openclaw-rules
featured: false
draft: false
tags:
  - AI
  - Tools
  - Thoughts
description: 记录我如何配置 OpenClaw 的记忆、权限和工作流
---

用 OpenClaw 用了一段时间，总结出几条规矩，写下来备忘。

## 它知道什么

OpenClaw 有两层记忆：每天的原始日志，和一个长期的精华文件。我让它把重要的事——决策、项目状态、我的习惯——都写进去。会话重启后靠这个接续上下文，不用每次重新解释。

目前记着的：
- 用 `pnpm` 不用 `npm`，Python 项目用 `uv` + `pyproject.toml`
- 网络搜索走 Exa
- **blog**：这个博客，它只有 fork 的写权限，改内容要提 PR 给我审

## 权限边界

读可以随便读，写要我点头。

具体来说：`git push`、`git commit`、开 PR、删库——任何会改变远程状态的操作，都要先问我。本地读文件、看 log、查 diff，不用问。

原因很简单：读错了没损失，写错了可能麻烦。

## 写博客的流程

以后整理对话或写文章，它负责起草，我审完再发。它没有直接推送的权限，只能提 PR。

另外装了个 `humanizer` skill，专门去掉 AI 腔。AI 写的东西有固定的语气病——首先、值得注意的是、三段式排比——看多了烦。这个工具能识别并改掉这些模式。

## 为什么要立规矩

不是不信任，是习惯。代码 review 存在的原因不是程序员不靠谱，而是多一道眼睛总没错。OpenClaw 也一样——执行能力强，但判断边界在哪，还是得人来定。

规矩越清晰，协作越顺。
