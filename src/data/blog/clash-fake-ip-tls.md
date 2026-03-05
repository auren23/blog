---
author: Xeron
pubDatetime: 2026-01-18T00:00:00Z
title: Clash Fake IP 导致 TLS 握手失败
slug: clash-fake-ip-tls
featured: false
draft: false
tags:
  - Linux
  - Network
  - Troubleshooting
description: 在使用 Clash Fake IP 模式时遇到 TLS 握手失败问题的排查与解决方案
---


在使用 paru 安装 AUR 包时遇到了 `TLS connect error: error:0A000126:SSL routines::unexpected eof while reading` 错误，即使开启了 TUN 模式全局代理也无法解决

## 问题现象

安装 google-chrome-canary 时下载失败：

```bash
paru -S google-chrome-canary
# curl: (35) TLS connect error: error:0A000126:SSL routines::unexpected eof while reading
# ERROR: Failure while downloading https://dl.google.com/linux/chrome/deb/...
```

## 诊断过程

### 1. 检查代理状态

```bash
curl ipinfo.io
# 显示美国 IP，说明代理正常工作
```

### 2. 检查 DNS 解析

```bash
nslookup dl.google.com
# Name:    dl.google.com
# Address: 198.18.0.15  ← 这是 Fake IP！
```

### 3. 测试 TLS 握手

```bash
curl -v https://dl.google.com/linux/chrome/deb/pool/main/g/google-chrome-canary/google-chrome-canary_146.0.7637.0-1_amd64.deb -o /tmp/test.deb
# * Trying 198.18.0.15:443...
# * TLSv1.3 (OUT), TLS handshake, Client hello (1):
# * TLS connect error: error:0A000126:SSL routines::unexpected eof while reading
```

## 问题根源

Clash Meta 的 **Fake IP 模式**在处理某些域名的 TLS 握手时存在兼容性问题：

1. Clash 为 `dl.google.com` 返回假 IP `198.18.0.0/16` 段地址
2. curl 连接到假 IP，Clash 应该透明代理到真实服务器
3. TLS 握手阶段，Clash 的处理出现异常（可能是 SNI 或证书验证相关）
4. Google CDN 检测到异常握手后主动断开连接

## 解决方案

### 方案 1：修改 Clash 配置（推荐）

编辑 Clash 配置文件（`~/.config/clash/config.yaml` 或 `~/.config/mihomo/config.yaml`）：

```yaml
dns:
  fake-ip-filter:
    - 'dl.google.com'
    - '*.dl.google.com'
```

重启 Clash 后，`dl.google.com` 将使用真实 IP 而不是 Fake IP

### 方案 2：使用浏览器下载

浏览器的 TLS 实现可能不受影响，可以直接下载：

1. 浏览器打开下载链接
2. 下载完成后手动安装：

```bash
cd ~/Downloads
ar x google-chrome-canary_*.deb
tar xf data.tar.xz
sudo cp -r opt/google/chrome-canary /opt/
sudo cp -r usr/* /usr/
```

### 方案 3：临时切换到 Real IP 模式

如果 Clash 支持模式切换，可以临时改为 Real IP 模式下载完成后再切换回来

### 方案 4：手动指定真实 IP

```bash
# 查询真实 IP
dig @1.1.1.1 dl.google.com +short

# 添加到 hosts（假设真实 IP 是 142.250.x.x）
sudo sh -c 'echo "142.250.x.x dl.google.com" >> /etc/hosts'

# 下载完成后删除该行
sudo sed -i '/dl.google.com/d' /etc/hosts
```