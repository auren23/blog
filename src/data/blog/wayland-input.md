---
author: Xeron
pubDatetime: 2025-08-30T00:00:00Z
title: Wayland 输入法配置
slug: wayland-input
featured: false
draft: false
tags:
  - Linux
  - Wayland
  - Input
description: Wayland 下输入法配置和常见问题解决方案
---


在 Wayland + Electron + 中文输入法（如 Fcitx5）环境中，部分应用在高频打字时会出现输入事件被乱序处理的现象：打字速度快会错位、重排，慢速输入则一切正常。该问题可在多款 Electron 应用中复现，与 Electron 在 Wayland/XWayland 下的输入通道与合成策略有关

相关讨论可参考：

- [Cherry Studio: Linux 的 Wayland 下不能切换 Fcitx5 输入法 #104](https://github.com/CherryHQ/cherry-studio/issues/104)

## 解决方案

为 Electron 应用启用原生 Wayland IME 支持与 Ozone 平台特性。创建（或编辑）文件 `~/.config/electron-flags.conf`，写入以下内容：

```
--enable-wayland-ime
--enable-features=WaylandWindowDecorations
--ozone-platform-hint=auto
--enable-features=UseOzonePlatform
--ozone-platform=wayland
```

保存后，完全退出并重新启动目标 Electron 应用。大多数 Electron 应用会自动读取该文件并追加这些运行参数，从而在 Wayland 下启用原生输入法通道，避免高频输入时的乱序问题

## 说明与提示

- 以上配置适用于常见的 Electron 应用（AppImage、.deb、.rpm、Flatpak 版本多数同样适用）
- 如应用仍以 XWayland 方式运行，确保会话/启动器未强制 `--ozone-platform=x11`，并优先保持 `wayland`
- 对于 Fcitx5 与 IBus 均有正向帮助；若你使用 Hyprland、Sway、KDE Wayland 等合成器，均可参考本方法
