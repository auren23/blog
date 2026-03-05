---
author: Xeron
pubDatetime: 2024-11-14T00:00:00Z
title: Wayland 下 Neovim 剪贴板配置
slug: nvim-clipboard
featured: false
draft: false
tags:
  - Neovim
  - Linux
  - Wayland
description: Wayland 环境下配置 Neovim 剪贴板共享的完整方案
---


在使用 Nvim 删除文本并尝试粘贴时，我发现 `d` 键删除文本后再粘贴我刚复制的文本粘贴不上

### 问题分析

刚开始，我以为是 Nvim 与 `wl-clipboard` 之间不能交互，尝试将以下配置添加到 `~/.config/nvim/init.lua` 文件中

```lua
vim.opt.clipboard = "unnamedplus"
```

然而，这并没有解决问题。`d` 键删除文本时，依然会将文本复制到剪贴板

### 解决方案

在 Nvim 中使用 d 删除文本时，删除的内容会同时被放入 Nvim 的默认寄存器和系统剪贴板寄存器

在 `~/.config/nvim/init.lua` 中添加以下配置来禁用删除时自动复制到剪贴板：

```lua
-- 禁用删除时自动复制到剪贴板
vim.api.nvim_set_keymap('n', 'd', '"_d', { noremap = true })
vim.api.nvim_set_keymap('n', 'D', '"_D', { noremap = true })
vim.api.nvim_set_keymap('n', 'dd', '"_dd', { noremap = true })
```
