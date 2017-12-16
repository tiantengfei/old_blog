---
layout: post
title: 极大似然估计与kl散度
description: "Maximizing likelihood is equivalent to minimizing KL-Divergence"
tags: [deeplearning]
category: deeplearning
imagefeature: cover6.jpg
comments: true
share: true
---

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

使用kl散度来解释极大似然估计。极大似然估计其实就是极小化kl散度。由于kl散度的最小值为零，
所以使用极大大似然估计作为损失函数，损失最小为零。在deeplearningbook5.5中进行了推导。

极大似然估计的特点：
* ##### 当训练样本的数量接近无穷，极大似然估计能够获得真实分布的参数。
    需要满足一下的条件
    * 真实的分布必须包含在$$p_{model}(\cdot ;\Theta )$$
    * 真实的数据分布必须只有一组对应的$$\Theta$$



### 参考
* [Maximizing likelihood is equivalent to minimizing KL-Divergence](https://wiseodd.github.io/techblog/2017/01/26/kl-mle/)
