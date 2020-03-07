---
layout:     post
title:      KL散度_JS散度_Wasserstein距离
subtitle:   KL散度_JS散度_Wasserstein距离的简单理解与介绍
date:       2020-03-07
author:     TkiChus
header-img: img/post-bg-KL.jpg
catalog: true
tags:
    - TkiChus
    - DreamMemory001 Blog
    - MachineStudy
---



# KL散度

> KL散度又称为相对熵，信息散度，信息增益。KL散度是俩个概率分布P和Q之间差别的非对称性之间的度量，KL散度是用来度量使用基于Q的编码来编码来自P的样本平均所需的为的位元数。典型情况下，P表示数据的真实分布，Q表示数据的理论分布，模型分布，或P的近似分布。

定义如下：

![KL散度](http://ww1.sinaimg.cn/large/006nBCHPly1gcl9sb13gmj30gu030jrm.jpg)

KL散度主要的俩个性质：

（1）不对称性：

尽管KL散度从直观上是个度量或距离函数，但他并不是一个真正的度量或者距离，因为他不具有对称性，即D(P||Q)!=D(Q||P)。

（2）非负性：

相对熵的值是非负的，因为对数函数是凸函数，所以非负即D(P||Q)>0。

# JS散度

> JS散度度量俩个概率分布的相似度，基于KL散度的变体，解决了KL散度非对称的问题，一般地，JS散度是对称的，其取值是0到1之间。

![JS散度](http://ww1.sinaimg.cn/large/006nBCHPly1gcla2lvdenj30ik02zwej.jpg)

KL散度和JS散度度量时候的一个问题：

如果俩个分配P,Q离得很远，完全没有重叠的时候，那么KL散度值是没有任何意义的，而JS散度值是一个常数值。这在学习算法中是比较致命的，这就意味着这一点的梯度值为0,。梯度消失了。

# Wasserstein距离

>  Wasserstein距离度量是俩个概率分布之间的距离，

![Wasserstein距离](http://ww1.sinaimg.cn/large/006nBCHPly1gcla7rymsnj30cu02ct8p.jpg)

![3.png](http://ww1.sinaimg.cn/large/006nBCHPly1gclay4rk4cj30s703tq3p.jpg)

Wessertein距离相比KL散度和JS散度的**优势**在于：即使两个分布的支撑集没有重叠或者重叠非常少，仍然能反映两个分布的远近。而JS散度在此情况下是常量，KL散度可能无意义。

## 总结：

三者都是用来衡量两个概率分布之间的差异性的指标。不同之处在于它们的数学表达。

























