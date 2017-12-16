---
layout: post
title: Deep Semantic Hashing with Generative Adversarial Networks
description: "Deep-Semantic-Hashing-with-Generative-Adversarial-Networks"
tags: [deeplearning]
category: deeplearning
imagefeature: cover6.jpg
comments: true
share: true
---

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

在 [Deep Semantic Hashing with Generative Adversarial Networks](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=0ahUKEwjq89nB7YvYAhVOxmMKHV9pBLcQFgguMAA&url=https%3A%2F%2Fwww.microsoft.com%2Fen-us%2Fresearch%2Fwp-content%2Fuploads%2F2017%2F06%2Ffp475-qiuA.pdf&usg=AOvVaw3C8rnNxAseM0iWJJdElmQ2)的论文中，作者用ＧＡＮ实现了一个半监督的 end to end 的网络架构DSH-GANS(DEEP SEMANTIC HASHING WITH GANS)实现了图片的检索(image retrieval)。在实现中作者使用了３种损失函数组成了最终的损失函数，分别是classfication loss、adversarial loss、triplet ranking loss。

#### １. 网络的架构
![网络架构](/images/gans/DSH-GANS_1.png)

**<center>图一　网络架构</center>**

如图一所示，网络的输入为真实图片和合成图片组成的real-synthetic的triplets组成。每个triplets包含一张真实图片，一张和真实图片同label的的合成图片，一张和真实图片不同label的合成图片。这些图片用同一个卷积神经网络去获取图片的representation。

在学习到respresentation后，使用３个stream（实际上是３个方面）去学习，分别是classfication stream、hash stream、adversary stream，对应着３个损失函数: classfication loss、triplet ranking loss、adversarial loss。

##### 1.1 classfication stream

 图片的label不仅提供了图片的类别信息，也提供了图片的语义结构(semantic structure),为了更好的在生成图片hash能够映射出图片之间的语义相似，加入了classfiction stream。在单标签的分类问题中，使用softmax函数，损失函数为:  

![classfication loss](/images/gans/DSH-GANS_equation.png)

在多分类问题中，使用sigmod函数，损失函数为：

![多分类loss](/images/gans/DSH-GANS_equation1.png)

#### 1.2 hash stream
在以往，使用representation的方法学习图片的hash code，往往独立的考虑每张图片，没有考虑到图片之间的相似与不相似性。而在图片检索中，这种信息很重要。作者利用了图片之间的相似性来获取图片的hash。我们容易获取<a href="https://www.codecogs.com/eqnedit.php?latex=\left&space;(&space;x,x^{&plus;},^{x-}\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\left&space;(&space;x,x^{&plus;},x^{-}\right&space;)" title="\left ( x,x^{+},^{x-}\right )" /></a>这样的triplet,其中ｘ为真实图片，<a href="https://www.codecogs.com/eqnedit.php?latex=x^{&plus;}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x^{&plus;}" title="x^{+}" /></a>为和ｘ同标签的生成图片。<a href="https://www.codecogs.com/eqnedit.php?latex=x^{-}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x^{-}" title="x^{-}" /></a>为ｘ不同标签的生成图片。使用<a href="https://www.codecogs.com/eqnedit.php?latex=H\left&space;(&space;x&space;\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?H\left&space;(&space;x&space;\right&space;)" title="H\left ( x \right )" /></a>对图片进行hash编码，当<a
 href="https://www.codecogs.com/eqnedit.php?latex=x_{i}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_{i}" title="x_{i}" /></a>中大于0.5时，当<a
  href="https://www.codecogs.com/eqnedit.php?latex=x_{i}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_{i}" title="x_{i}" /></a>中大于0.5时为１，否则为０，所以triplet loss函数为：

  ![triplet loss](/images/gans/DSH-GANS_equation2.png)

  上面的损失函数是使用汉明距离来计算损失的，但是这个函数不是smooth的，在某些位置不可导，所以对上面的损失函数进行了ease,使用Ｌ2-norm来计算代替距离。具体如下：

  ![triplet loss](/images/gans/DSH-GANS_equation3.png)

#### 1.3 Adversary stream
生成网络的损失由<a href="https://www.codecogs.com/eqnedit.php?latex=\left&space;(&space;x,x^{&plus;},^{x-}\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\left&space;(&space;x,x^{&plus;},x^{-}\right&space;)" title="\left ( x,x^{+},^{x-}\right )" /></a>中每个图片的loss相加得到，如下：

![triplet loss](/images/gans/DSH-GANS_equation4.png)

其中：
![triplet loss](/images/gans/DSH-GANS_equation5.png)

### ２．优化

对于共享的CNN网络，优化目标为：


![triplet loss](/images/gans/DSH-GANS_equation6.png)

对于生成网络来说，优化目标为：

![triplet loss](/images/gans/DSH-GANS_equation7.png)

#### ３．总结
作者提出了一个半监督的图片检索方法，不仅保留了图片之间的相对相似性还保留了图片之间的语义信息。


#### 参考文献
[Deep Semantic Hashing with Generative Adversarial Networks](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=0ahUKEwjq89nB7YvYAhVOxmMKHV9pBLcQFgguMAA&url=https%3A%2F%2Fwww.microsoft.com%2Fen-us%2Fresearch%2Fwp-content%2Fuploads%2F2017%2F06%2Ffp475-qiuA.pdf&usg=AOvVaw3C8rnNxAseM0iWJJdElmQ2)
