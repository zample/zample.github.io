---
title: Kullback-Leibler散度
layout: post
categories: Microeconometrics
tags: 统计学习
mathjax: 'true'
---
## Kullback-Leibler散度

当我们有两个分布$p(x)$和$q(x)$，如何衡量它们之间的相似性？

​	可通过计算它们的Kullback-Leibler散度（Kullback-Leibler divergence），以下简称为KL散度。KL散度的引入由信息论得来，这里不作介绍。KL散度的计算方式为：
$$
KL(p||q)=\int p(x)\ln\frac{p(x)}{q(x)}dx \tag{1}
$$
​	KL散度具有以下几种性质：

1. KL散度不是一个对称量，即$K L(p \Vert q) \neq K L(q \Vert p)​$，可从定义可得出

2. $KL(p\Vert q)\geqslant 0​$， 证明如下：

   $$
   \begin{split}
   KL(p||q) &= \int p(x)\ln\frac{p(x)}{q(x)}dx \\
   &=\int p(x) (-\ln\frac{q(x)}{p(x)})dx \\
   &\geqslant - \ln \int p(x) \frac{q(x)}{p(x)}dx \quad \textrm{（Jenson不等式，$-\ln{x}$是凸函数）}\\
   &= 0
   \end{split}
   $$

3. 当$p(x)=q(x)$时，KL散度为0，即KL散度达到最小。


### $KL(p\Vert q)$与$KL(q\Vert p)​$的不对称性

​	考虑一种较为特殊的情形：分布$p(x)​$和$q(x)​$均为高斯分布，它们拥有相同的均值，其中$q(x)​$的方差较小，而$p(x)​$的方差较大，它们的概率密度函数图如下所示：

![figure1](https://github.com/zample/zample.github.io/blob/master/screenshot/blog/kldivergence/figure1.jpg?raw=true)

​	如何比较$KL(p\Vert q)$与$KL(q\Vert p )$的大小？

​	一种直观的估计，根据公式$KL(p\Vert q)=\int p(x)\ln\frac{p(x)}{q(x)}dx$，尽管在$p(x)<q(x)$的区域里，积分为负值，但在$p(x)>q(x)$的区域中，$q(x)$比$p(x)$更快地趋近于0，使得$\frac{p(x)}{q(x)}$有更大的值（例如0.01/0.001）；而在$KL(q\Vert p)=\int q(x)\ln\frac{q(x)}{p(x)}dx$中，在$p(x)$小于$q(x)$的区域中，$\frac{q(x)}{p(x)}$的值通常不会太大（例如0.8/0.4），故在此例中，$KL(p\Vert q)>KL(q\Vert p )$。

​	考虑一种稍为复杂的情况：$p(x)​$为给定的双峰高斯分布，$q(x)​$为单峰高斯分布，考虑3种不同的q(x)，如下图所示：（蓝线代表$p(x)​$，红线代表$q(x)​$。）

![figure2](https://github.com/zample/zample.github.io/blob/master/screenshot/blog/kldivergence/figure2.jpg?raw=true)

​	若计算$KL(p\Vert q)​$，则在前两种情况KL散度更大（$q(x)​$尾部概率比$p(x)​$更快地趋于0），而最后一种情况KL度较小（$KL(p\Vert q)=(43.9, 15.4, 0.97)​$）。若计算$KL(q\Vert p)​$，则前两种情况散度更小，而最后一种情况KL散度更大（$p(x)​$尾部概率比$q(x)​$更快地趋于0）（$KL(q\Vert p)=(0.69, 0.69, 3.45)​$）。

​	考虑到KL散度衡量两个分布的相似度，KL散度越小，我们认为两个分布之间越相似（越接近）。在给定$p(x)$的情况下，通过最小化KL散度来得到与$p(x)$最接近的一元高斯分布。若按$KL(p\Vert q)$度量，则我们认为第三种情况下的$q(x)$更接近$p(x)$；若按$KL(q\Vert p)$度量，则我们认为前两种情况下的$q(x)$更接近$p(x)$。（事实上图中所画的三种$p(x)$中前两种为$KL(q\Vert p)$局部极小，后一种为$KL(p\Vert q)​$局部极小）。