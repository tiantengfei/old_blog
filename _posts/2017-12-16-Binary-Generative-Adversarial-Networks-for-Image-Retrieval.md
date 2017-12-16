---
layout: post
title: Binary Generative Adversarial Networks for Image Retrieval
description: "Binary Generative Adversarial Networks for Image Retrieval"
tags: [deeplearning]
category: deeplearning
imagefeature: cover6.jpg
comments: true
share: true
---

在本文中，作者提出了BGAN(binary generative adversarial networks)，利用无监督的方式实现了图片检索。   
在文中作者主要解决了两个问题：  
* 如何在没有relaxation下的情况下，生成图片的hash（二进制）表示。
* 如何利用hash实现准备的图片检索。  

作者通过设计了新的激活函数和目标函数解决了这个问题。

#### 1. 网络架构

![BGANS架构](/images/gans/BGANS_1.png)
**<center>图一　网络架构</center>**

如上图所示，这个架构主要由４部分组成:　　
1. encoder:学习图片的表示(image representation)
2. hash layer: 生成Ｌ-bit的hash码　　
5. decoder: 用生成网络由hash码重新构造图片　　
7. discriminator: 判别是真实图片还是生成的图片

##### 1.1 encoder
和VGG19相似，５个卷积层和５个max pooling层。
##### 1.2 hasing
将从encoder学习到的L-demension的表示转变为二进制编码，函数表示为：  

![bgan](/images/gans/BGANS_equation.png)  

其中Z为得到L-demension的图片representation.  

上面的sgn函数是non-smooth和non-convex，所有的非零的输入梯度为零，所以这个函数在零处是ill-defined,这会引起梯度消失的问题。作者通过随着训练过程，逐渐的减少目标函数的smooth。最终的结果将收敛到预期的目标函数。定义了一个函数app(.)去逼近sgn(.):

![bgan_1](/images/gans/BGANS_equation1.png)

sgn(.)和app(.)之间存在下面的关系：  

![bgan_2](/images/gans/BGANS_equation2.png)

当<a href="https://www.codecogs.com/eqnedit.php?latex=\beta&space;\rightarrow&space;\infty" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\beta&space;\rightarrow&space;\infty" title="\beta \rightarrow \infty" /></a>时，app(.)逼近sgn(.)

##### 1.3 Generator和Discriminator
生成网络根据图片的hash code去生成图片。

#### 2. 优化
作者使用了３种损失函数,分别是neighbors structure loss、content loss、　adversarial loss。
#### 2.1 Neighbors Structure Loss  

作者对每一张图片使用2048 dimensions的向量表示，利用ｋ-nearest来构建相似度矩阵S，如果图片i、ｊ是相似的，则<a href="https://www.codecogs.com/eqnedit.php?latex=S_{ij}=1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S_{ij}=1" title="S_{ij}=1" /></a>，否则<a href="https://www.codecogs.com/eqnedit.php?latex=S_{ij}=-1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S_{ij}=-1" title="S_{ij}=-1" /></a>。由于ｋ的增加会减少矩阵的精度，所以作者提出了如果图片ｉ与图片ｊ相似，图片ｊ与图片ｈ相似，则图片ｉ与ｈ也相似的方式来扩展矩阵Ｓ。扩展的方式利用两张图片对应的列相似，计算方法为<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{1}{\left&space;\|S_{i}&space;-&space;S_{j}&space;\right&space;\|^{2}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{1}{\left&space;\|S_{i}&space;-&space;S_{j}&space;\right&space;\|^{2}}" title="\frac{1}{\left \|S_{i} - S_{j} \right \|^{2}}" /></a>
。假设所有图片的hash表示为<a href="https://www.codecogs.com/eqnedit.php?latex=B=^{\left&space;\{&space;b_{i}&space;\right&space;\}_{1}^{N}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?B=^{\left&space;\{&space;b_{i}&space;\right&space;\}_{1}^{N}}" title="B=^{\left \{ b_{i} \right \}_{1}^{N}}" /></a>,则neighbors structure loss为:  

![equation3](/images/gans/BGANS_equation3.png)  

#### 2.2 content loss
content loss是两张图片之间的pixel-wise的损失和图片在判别网络最后一个卷积层的输出作为表示的欧几里得距离。
pixel－wise之间的损失为：  

![equation４](/images/gans/BGANS_equation4.png)  
　

图片在判别网络最后一个卷积层的输出作为表示的欧几里得距离为:  

![equation5](/images/gans/BGANS_equation5.png)　　

所以content loss为:  

![equation6](/images/gans/BGANS_equation6.png)  

#### 2.3 Adversarial loss
Ｄ为判别网络，<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{200}&space;I^{R}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{110}&space;I^{R}" title="I^{R}" /></a>表示生成网络G生成的图片。  

　![equation7](/images/gans/BGANS_equation7.png)

所以整个网络的损失函数为:  

![equation8](/images/gans/BGANS_equation8.png)  

#### 3.总结
作者提出了无监督的hash方法，主要解决了不在relaxation的情况下如何直接生成图片的hash和如何使得生成的hash能够准确的实现image Retrieval。
