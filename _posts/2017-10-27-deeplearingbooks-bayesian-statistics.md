---
layout: post
title: 贝叶斯统计
description: "Bayesian Statistics"
tags: [deeplearning]
category: deeplearning
imagefeature: cover6.jpg
comments: true
share: true
---

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

frequentist statistics:估计出一个c,然后用$$\Theta$$来做预测。

bayesian statistics:预测的时候，考虑$$\Theta$$所有可能的值。

在贝叶斯统计中， $$\Theta$$ 被视为一个随机变量。

#### 贝叶斯和极大似然估计的不同：
* 极大似然估计用点估计估计$$\Theta$$值，而贝叶斯考虑了所有可能的$$\Theta$$，在观测了
m样本后，预测m+1个样本。
   ![Bayesian statistics]({{site.url}}/images/deeplearingbooks/bayesian_statistics_1.png)
* 贝叶斯提供了一个先验概率

在小数据上，贝叶斯泛化效果更好，但是计算量大。

### 参考
* [chaptor 5.6 deeplearning book](http://www.deeplearningbook.org/contents/ml.html)
