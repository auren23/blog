---
author: Xeron
pubDatetime: 2024-06-22T00:00:00Z
title: Neovim 查找替换技巧
slug: neovim-replace
featured: false
draft: false
tags:
  - Neovim
  - Editor
  - Linux
description: Neovim 中实现高效查找替换的技巧和命令
---


## Neovim批量替换文本

在nvim中输入

```
:args file1.txt file2.txt file3.txt #加载文件
:argdo %s/pattern/replacement/g
```

或是使用[nvim-spectre](https://github.com/nvim-pack/nvim-spectre)插件
