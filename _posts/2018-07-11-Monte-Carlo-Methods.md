---
layout: post
title: Monte-Carlo-Methods
description: ""
tags: [deeplearning]
category: deeplearning
imagefeature: cover6.jpg
comments: true
share: true
math: true
---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;随机算法共分为两类:(1)拉斯维加斯算法(Las Vegas algorithms):总是返回精确的结果(2)蒙特卡洛方法(Monte Carlo Methods ):提供近似的结果。机器学习中，很多问题是难以计算出准确的结果，这时就需要蒙特卡洛等近似算法。蒙特卡洛算法通过采样得到难以计算的求和或者积分的结果，大大的减少了基计算的难度。
#### 蒙特卡洛采样的基础
蒙特卡洛方法将求和或者积分问题看作求某一分布下的期望。
对于离散变量$X$:

$$s=$$
对于连续变量$X$:

$$s=$$

其中$p$随机变量$x$的分布。  
通过从概率分布$p$随机采样n个样本$x^{(1)},x^{(2)},....,x^{(n)}$等到s的近似值:  

$$s_n=\frac{1}{n}\sum_{i}^{n}{p(x^{(i)})f(x^{(i)})}$$

则可知$s_n$是s的[无偏估计](#unbias)，**无偏估计的计算如下**。  
由大数定律可知:

$$\lim_{n \to +\infty}s_n=s$$

同时也可知，当$n \to \infty$时，$var(s_n) \to 0$。$var(s_n)$的计算如下：

$$$$
由中心极限定理可知：平均分布$s_n$收敛到均值为$s$,方差为$\frac{var(f(x))}{n}$。


#### 重要性采样
上述的方法实现的基础是能够容易地从概率分布中采样的样本(是p不好找，还是不容易从p中采样数据?)。但是这样的情况并不总会发生。采取重要性采样(importance sampling)或者更加通用的蒙特卡洛马尔科夫链(Monte Carlo Markov chains)采样方法。
#### 附录
##### <a name="unbias"></a>无偏估计

##### <a name="central-limit-law"></a>中心极限定理






