---
author: Xeron
pubDatetime: 2025-01-18T00:00:00Z
title: 清理 Git 中的 __pycache__
slug: pycache-fix
featured: false
draft: false
tags:
  - Python
  - Git
description: 如何从 Git 仓库中清理误提交的 Python __pycache__ 缓存文件
---

`__pycache__` 文件夹包含 Python 的编译缓存文件（`.pyc` 等），通常不需要提交到 Git 仓库

## 1. 确保 `.gitignore` 文件中忽略**pycache**

在项目根目录的 `.gitignore` 文件中添加以下内容，确保 Git 忽略 `__pycache__`：

```txt
**/__pycache__/
```

## 2. 从 Git 仓库中移除**pycache**

从 Git 索引中移除已经提交的 `__pycache__`：

```bash
git rm -r --cached __pycache__

git commit -m "Remove __pycache__ from version control"

git push
```

## 3. 使用 BFG Repo-Cleaner 清除历史记录

如果 `__pycache__` 已经存在于 Git 的历史记录中，你可以使用 [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/) 来彻底清除它

### 安装 BFG Repo-Cleaner

arch用户可以通过 AUR 安装：

```bash
yay -S bfg-repo-cleaner
```

或者从其 [GitHub 页面](https://github.com/rtyley/bfg-repo-cleaner/releases) 下载 jar 文件

### 使用 BFG 清理

```bash
bfg --delete-folders '__pycache__' --no-blob-protection
```

运行完成后，会清理掉所有历史中的 `__pycache__` 文件夹

### 清理历史并优化

```bash
git reflog expire --expire=now --all

git gc --prune=now --aggressive
```

### 强制推送到远程仓库

```bash
git push --force
```
