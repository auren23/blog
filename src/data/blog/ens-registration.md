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


## Ens域名注册事项

打开[Ens](https://app.ens.domains/)，搜索想要的域名，比如说`test1234.eth`，我使用Binance的web3钱包，所以选择`WalletConnect`。也可以选择别的钱包，比如说MetaMask。建议一次注册5年以上，这样网络费只需支付一次，钱包里需要有以太坊主网的eth，别的链上的eth使用不了，一次最好多转一点eth，Ethereum(ERC20)网络转账手续费要4刀，多次转账损耗很多

注册时勾选作为主名称使用会解析你的钱包地址，注册好域名之后可以添加个人资料，可以去`yourname.eth.xyz`查看，每次更新资料都会有gas费

如果你要使用ens域名跳转静态博客网站之类的，可以用IPFS，将静态网站代码上传至IPFS然后填入ens域名的个人资料即可，也可以上传`index.html`跳转至你的网站

```html
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="refresh" content="0; url=https://yoursite" />
    </head>
    <body></body>
</html>
```

推荐使用[Fleek](https://fleek.xyz/)，使用IPNS链接方便后续更改，只需支付一次gas费

之后就可以使用Brave，Opera访问你的域名`yourname.eth`，也可以在Firefox，Chrome使用`yourname.eth.limo`访问，比如说我的域名`xeron.eth`就可以使用`xeron.eth.limo`在Firefox访问
