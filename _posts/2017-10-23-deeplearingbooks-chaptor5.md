---
layout: post
title: machine learning base
description: "machine learning base"
tags: [sample post]
imagefeature: cover6.jpg
comments: true
share: true
---

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
# 5.1 Learning Algorithm
* Task T
* Experience E
* Measure P
## 5.1.1 Tasks
* classfications
* classfication with missing inputs
* regression
* transcription
* machine translation
* Structured output
* Anomaly detection(异常检测)
* Synthesis and sampling
* Imputation of missing values
* Denoising(去噪)
* Density estimation or probability mass function estimation
## 5.1.2 The Perfermence P
  * what should be measured.
  * measuring it is impractical.
##  5.1.3 Experience
* 监督学习与无监督学习之间没有明显的界限
## 5.1.4 Linear Regression
* 矩阵的求导
* MSE
# 5.2 capacity,Overfiting and Underfitting  
如何由训练集能保证在测试集上有良好的效果?  
 statistical learning theory：假设训练集和测试集是独立同分布的。
所以能够使用一个概率分布来描述。
* 如何决定一个机器学习算法的好坏?  
  (1)使训练集最小  
  (2)使train error 和 test error之间的gap最小  
  这两点对应了机器学习中的overfitting和underoverfitting  
* capacity  
  通过修改模型的capacity去控制模型是否过拟合。  
  capacity表明了模型是否能够适应 wide variety of functions。  
  控制capacity:hypothesis space.      
* vc维
   * 测量一个二分类分类器的capacity.  
* Bayes error  
  不可避免的error.  
## 5.2.1 no free lunch theorem
  >让我们清楚地认识到，脱离具体问题，空泛地谈论”什么学习算法更好“毫无意义，因为若考虑所有潜在的问题，则所有的算法一样好.   
  要谈论算法的相对优劣，必须要针对具体问题；在某些问题上表现好的学习算法，在另一问题上却可能不尽如人意，学习算法自身的归纳偏好与问题是否相配，往往会起到决定性作用.
  --来自周志华机器学习

## 5.2.2 regularization
  * 减少泛化error
# 5.3 Hyperparameters and Validation Sets
## 5.3.1 cross-validation
  * k-fold cross validation
# 5.4 estimatots,bias and variance
## 5.4.1 point estimation
* function estimation

  被给x，预测y的值。

## 5.4.2 bias

 在bias和variance做trade off时的方法：（1）cross-validation (2)\(MSE=bias(x^2)\)

# 5.6 Maximum (MAP) Estimation

   很多正则化的策略能够被当做将MAP当做贝叶斯引用。
# 5.8 Unsupervised learning Algorithm
* pca以及奇异值分解 [参考](http://blog.csdn.net/zhongkelee/article/details/44064401)

# 5.11 深度学习中的挑战
* 高纬度的数据 the curse of dimensionality
* smoothness prior or local constancy prior.
* manifold learning
