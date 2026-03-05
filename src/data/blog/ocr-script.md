---
author: Xeron
pubDatetime: 2024-10-16T00:00:00Z
title: Python OCR 自动化脚本
slug: ocr-script
featured: false
draft: false
tags:
  - Python
  - OCR
  - Automation
description: 使用 Python 和 Tesseract 实现自动化 OCR 文字识别脚本
---

在hyprland一直没找到舒服的OCR的软件，先使用这个脚本代替一下

## 所需软件

要运行 `ocr_screenshot.sh` 脚本，需要安装以下软件包：

1. **Tesseract**：用于从图像中提取文本的 OCR 引擎
2. **Grim**：在 Wayland 中截取屏幕的工具
3. **Slurp**：在 Wayland 中选择屏幕区域的工具
4. **wl-clipboard**：用于在 Wayland 中操作剪贴板的工具

### 安装命令

在终端中运行以下命令以安装所需的软件：

```bash
sudo pacman -S tesseract grim slurp wl-clipboard
```

### 脚本内容

```bash
#!/bin/bash

# Take a screenshot with Grim and Slurp
grim -g "$(slurp)" /tmp/screenshot.png

# Perform OCR with both Chinese and English language support and copy the result to clipboard
tesseract /tmp/screenshot.png - -l chi_sim+eng | wl-copy

# Optionally, remove the screenshot file
rm /tmp/screenshot.png
```

### 赋予执行权限和移动脚本

1. 将 `ocr_screenshot.sh` 脚本保存到主目录（如 `~/ocr_screenshot.sh`）
2. 赋予脚本执行权限：

    ```bash
    chmod +x ~/ocr_screenshot.sh
    ```

3. 移动脚本到 `/usr/local/bin` 目录：

    ```bash
    sudo mv ~/ocr_screenshot.sh /usr/local/bin/
    ```

## Hyprland 配置

1. 打开Hyprland 配置文件，通常位于 `~/.config/hypr/hyprland.conf`

2. 添加以下行，将 `SUPER + O` 键组合绑定为执行 `ocr_screenshot.sh` 脚本：

    ```
    bind = SUPER, O, exec, ocr_screenshot.sh
    ```
