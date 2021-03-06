+++
title = "Skycoin 会被51%攻击吗？"
tags = [
    "Statement",
    "Obelisk",
    "Consensus",
]
bounty = 8
date = "2017-10-07"
categories = [
    "Statement",
]
+++

*这是2015年2月16日在bitcointalks上讨论的存档*

> 引自: **iamback** (2015-02-16 09:28:38 AM)

> 非PoW共识是DOA，因为没有足够的时间来剔除和信任在2016年全球经济开始崩溃之前的问题。例如，自私采矿攻击没有被发现（或者说广泛地证明和认可），直到Satoshi发表PoW的几年。 就这样严肃的市场不会相信一个全新的非PoW共识算法。相反，我设计了一个PoW系统，该系统解决了困扰比特币的问题，包括ASIC挖矿经济. 有一些小分享在我的链接的帖子上.

> 同样的我也有一些在数学方面的直觉，那就是避免51%攻击总会在其他的安全问题方面有妥协

Skycoin中51%攻击无关紧要. skycoin网络每天都有20多次的51%攻击但是几乎没人关心这个.

Skycoin 与 Bitcoin相比有不同的数学性质并且更严格. 如果你在一个封闭网络中在5个人之间来来回回的进行交易，51%攻击不会影响到他们. 为了能在skycoin 51%攻击上搞破坏，你需要得到这条交易链某个人的私钥. skycoin没有交易延展性攻击. 几乎每个人在原链和分叉的链上有一样的输出和相同的余额和相同的交易历史，除了攻击者和与他进行交易的人. 如果链上有分叉，skycoin仅仅从其他的链上拷贝交易.

51％攻击只会影响与阴暗的人交易的人和赌博网站。 它对商业交易的影响有限。 如果交易所遵循最佳的安全实践，保持与用户钱包隔离，他们最严重的攻击造成的影响也是很轻微的。

比特币每天有一亿美元的交易量. 总的比特币的交易量约为20万枚.  比特币有交易延展性，这意味着如果有人51％攻击和回滚最后一小时交易，然后约400万美元和10000枚比特币被搞砸了。 回滚攻击24小时可以造成一亿美元的损失总共20万枚比特币. 攻击者可以回滚比特币中的任何交易.

Skycoin中，攻击者在不知道那条交易链上某个地址的私钥的时候不能影响或者修改交易链.  因此如果5个银行之间只是来回交易转让并且他们的钱包都安全，51%攻击甚至都不能察觉到. 他们的余额是相同的. 也就是说，51%攻击在数学上说是可能的，有人把资源浪费在上面尝试它然后成功了。

如果有人试图对skycoin进行51%攻击（这是有可能的，但是在数学意思上说是不可能的)商人会唱歌跳舞欢庆，因为损失会比Visa费率低低太多. 许多商家出售笔记本电脑，每台笔记本电脑的利润率不到5%. 有人声称他们没有得到笔记本电脑然后商人损失1000美元，没有找回笔记本电脑还得给Visa交80美元的费用. 公司需要卖出25台笔记本电脑才能弥补这一欺诈消费行为带来的的损失. 如果有人盗取了信用卡并且用来买了笔记本电脑, Visa不会承担损失，Visa会将损失转嫁给商人.

Skycoin的共识算法和账本是分开的. 共识系统是模块化的，可以换出. 如果5年过后有更好的算法, 我们仅仅只需替换为新的共识算法. 账本和余额保持不变.

Skycoin:

- 修复了比特币现有的问题
- 被证明了的未来的比特币
- 消除了比特币所设计的死亡螺旋条件（death spiral condition)

可以确信，会有很多妥协. 例如，快速的共识时间对像Skycoin类型相关的共识算法意味着发动对网络发动DDoS需要的节点数更少. 然而，人们可以对这种行为做出反应并将攻击节点从信任列表中移除.

会有问题，需要解决。

## Skycoin交易结构

https://github.com/skycoin/skycoin/blob/master/src/coin/transactions.go

Skycoin交易是:

1) 一系列的输出的哈希被发送

2) 一系列的签名认证消费(内部交易的哈希签名)的输出

3) 一系列的输出被创建

天空币不能被创建和销毁. 输入币的数量必须和输出的输出的数量相等. 交易费用是币龄（coinhour）.

## 天空币原生支持coinjoin

- 两个人选择他们想花费的输出, 他们像创建的输出, 发送给远程服务器.
- 服务器创建交易并打乱交易输入输出的顺序。然后发送给每个人
- 每个人将输出的签名发送到服务器
- coinjoin服务器将交易注入到网络

- coinjoin服务器不能盗取天空币
- 只有coinjoin服务器知道有多少人参与(1,2,4?)
- 只有coinjoin服务器知道哪个输出属于谁
- 正常交易和coinjoin交易没有区别（他们看起来确实一样）

“i”插槽中的签名对应拥有“i”输出的地址。这个交易的内部哈希会与被花费输出的哈希进行哈希，然后使用拥有这个输出的私钥进行签名.

因此，这与其他coinjoin系统相比起来非常简单.
