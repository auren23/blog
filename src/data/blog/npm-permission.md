---
author: Xeron
pubDatetime: 2025-12-11T00:00:00Z
title: 解决 npm 全局安装权限问题
slug: npm-permission
featured: false
draft: false
tags:
  - Node.js
  - NPM
  - Linux
description: 解决 Linux 下 npm 全局安装权限问题的正确方法
---


在使用 `npm update -g` 或 `npm install -g` 安装全局包时，遇到了 `EACCES: permission denied` 错误

## 问题分析

错误信息显示 NPM 尝试写入 `/usr/lib/node_modules` 目录时被拒绝，这是一个系统目录，普通用户没有写入权限

```bash
npm error code EACCES
npm error syscall rename
npm error path /usr/lib/node_modules/npm/node_modules/env-paths
npm error errno -13
npm error Error: EACCES: permission denied
```

虽然可以使用 `sudo` 来临时解决，但这会导致安全问题和权限混乱，最佳实践是将 NPM 的全局目录迁移到用户主目录

## 解决方案

### 1. 创建用户级全局目录

在终端中创建一个属于你的目录来存放全局包：

```bash
mkdir ~/.npm-global
```

### 2. 配置 NPM 使用新目录

修改 NPM 配置，让它使用刚创建的目录：

```bash
npm config set prefix '~/.npm-global'
```

### 3. 添加到环境变量

首先确认你使用的 Shell 类型：

```bash
echo $SHELL
```

根据结果编辑对应的配置文件：

- 如果是 `/bin/bash`，编辑 `~/.bashrc`
- 如果是 `/bin/zsh`，编辑 `~/.zshrc`

在文件末尾添加以下内容：

```bash
export PATH=~/.npm-global/bin:$PATH
```

### 4. 使配置生效

重新加载 Shell 配置：

```bash
source ~/.bashrc
# 或者
source ~/.zshrc
```

### 5. 重新安装全局包

现在可以不使用 `sudo` 直接安装全局包了：

```bash
npm install -g @musistudio/claude-code-router
```
