---
layout: post
title: 极大似然估计与kl散度
description: "Maximizing likelihood is equivalent to minimizing KL-Divergence"
tags: [deeplearning]
category: deeplearning 
imagefeature: cover6.jpg
comments: true
share: true
mathjax: true
---

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

现代神经网络使用最大似然估计来训练：
* 不需要为每一个模型都设计一个损失函数（cross-entropy）
* 解决saturate的问题。因为exp函数在值很小的时候会saturate,但是log函数能够避免这个问题
*

极大似然估计的特点：
* ##### 当训练样本的数量接近无穷，极大似然估计能够获得真实分布的参数。
    需要满足一下的条件
    * 真实的分布必须包含在 $$p_{model}(\cdot ;\Theta )$$
    * 真实的数据分布必须只有一组对应的$$\Theta$$



### 参考
* [Maximizing likelihood is equivalent to minimizing KL-Divergence](https://wiseodd.github.io/techblog/2017/01/26/kl-mle/)
