---
author: Xeron
pubDatetime: 2024-08-02T00:00:00Z
title: ENS 域名注册指南
slug: ens-registration
featured: false
draft: false
tags:
  - Web3
  - ENS
  - Blockchain
description: ENS 域名注册完整指南，包括费用计算、注册流程和常见问题
---

## 注册流程

打开 [ENS](https://app.ens.domains/)，搜索域名，连接钱包（WalletConnect/MetaMask）

建议一次注册5年以上，网络费只需支付一次。钱包需要以太坊主网的 ETH，ERC20 转账手续费约 4 刀，一次多转点

注册时勾选"作为主名称使用"会解析钱包地址。注册后可添加个人资料，在 `yourname.eth.xyz` 查看

## 绑定网站

用 IPFS 上传静态网站代码，填入 ENS 个人资料。或上传跳转页面：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="refresh" content="0; url=https://yoursite" />
    </head>
    <body></body>
</html>
```

## 访问方式

- Brave/Opera：直接访问 `yourname.eth`
- Firefox/Chrome：访问 `yourname.eth.limo`
