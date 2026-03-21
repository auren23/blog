---
author: Xeron
pubDatetime: 2026-03-21T00:00:00Z
title: gstack：把 Claude 变成一支工程团队
slug: gstack-breakdown
featured: false
draft: false
tags:
  - AI
  - Tools
  - Engineering
description: YC CEO Garry Tan 开源了他的 Claude Code 工作流。核心不是工具，是流程设计。
---

Garry Tan，YC 的 CEO，开源了他的 Claude Code 配置：[gstack](https://github.com/garrytan/gstack)。60天，60万行生产代码，同时全职跑 YC。数字有多少水分不重要，思路值得拆。

## 角色分工

把 Claude 当万能助手，上下文很快就乱了。gstack 的解法是把开发流程拆成职能角色，每个角色一个 slash command。

`/office-hours` 验证产品想法，`/plan-ceo-review` 质疑需求，`/plan-eng-review` 锁架构，`/review` 找生产 bug，`/ship` 管发布，`/qa` 真开浏览器点 app，`/retro` 给你看自己的 LOC 和 commit 数据。

每个角色上下文干净，不互相污染。

## 持久浏览器

`/qa` 背后是一个长驻 Chromium daemon。冷启动一次约3秒，之后每次调用 100-200ms，登录态和 tab 全部保留。打包成单一二进制，不依赖 node_modules。

传统方式每次 tool call 重开浏览器，慢且丢会话状态。持久 daemon 解决了这个问题。

## Skill 就是 Markdown

每个 skill 是一个 `SKILL.md`，YAML frontmatter 加自然语言指令。没有 SDK，没有框架。直接 prompt，模型读懂就执行。

## 湖 vs 海

gstack 有一条原则叫 Completeness Principle：

**湖**是有边界的任务，做完它。**海**是无边界的任务，建快捷方式，不强行完成。

防止 AI 把可以交付的任务无限膨胀。适用于 AI，也适用于你自己。

## 底层逻辑

gstack 在做一件事：把隐性的团队协作流程，显式地编码进 prompt。

CEO 问「为什么用户要用这个」，工程师问「这个架构三个月后能不能维护」。两种视角天然不同。gstack 把它们分开，强迫你在不同阶段用不同的思维框架。

这不是 Claude 的魔法，是流程设计。
