---
layout: post
title: machine learning base
description: "machine learning base"
tags: [sample post]
imagefeature: cover6.jpg
comments: true
share: true
---

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
*监督学习与无监督学习之间没有明显的界限
## 5.1.4 Linear Regression
* 矩阵的求导
* MSE
# 5.2 capacity,Overfiting and Underfitting
* 如何由训练集能保证在测试集上有良好的效果?</br> statistical learning theory：假设训练集和测试集是独立同分布的。
所以能够使用一个概率分布来描述。
* 如何决定一个机器学习算法的好坏?</br>
  (1)使训练集最小</br>
  (2)使train error 和 test error之间的gap最小</br>
  这两点对应了机器学习中的overfitting和underoverfitting
* capacity</br>
  通过修改模型的capacity去控制模型是否过拟合。</br>
  capacity表明了模型是否能够适应 wide variety of functions。</br>
  控制capacity:hypothesis space.
 * vc维
   测量一个二分类分类器的capacity.
  
* Bayes error</br>
  不可避免的error.

