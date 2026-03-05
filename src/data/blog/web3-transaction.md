---
author: Xeron
pubDatetime: 2025-01-25T00:00:00Z
title: 解决 Web3 交易 Underpriced 错误
slug: web3-transaction
featured: false
draft: false
tags:
  - Web3
  - Blockchain
  - Development
description: 解决以太坊交互中 "Replacement Transaction Underpriced" 错误的方法
---

## 昨天在Binance的web3钱包里交互时遇到了一个 "replacement transaction underpriced" 错误。通过提高gas费用解决


## 什么是 replacement transaction underpriced 错误？

与以太坊或其他 EVM 兼容区块链交互时，可能会遇到这样的错误："replacement transaction underpriced"。这个问题通常发生在试图用新的交易替换挂起的交易时，新交易的gas费设置得不够高，导致网络拒绝接收。以太坊网络支持"交易替换机制"（Transaction Replacement）。当一笔交易尚未被打包时，您可以发送一笔相同 nonce 的新交易来替换旧交易。但以太坊规定，新交易的gas费必须比旧交易至少高出10%。否则，矿工会拒绝处理这笔交易，从而产生replacement transaction underpriced 错误

## 可能的触发场景

1. 手动调整 Gas 费用过低：当替换交易时，未增加足够的 Gas 价格或动态费用

2. 网络拥堵：链上拥堵导致交易费大幅波动，新交易的费用不够吸引矿工

## 解决方法

1. 增加10%的gas费，替换上个交易

2. 如果不急着交易，等待上个交易完成再进行

3. 如果希望取消挂起的交易，可以创建一笔 相同 nonce 的新交易，将目标地址设置为自己的地址，金额设置为 0，并提高 Gas 费用
