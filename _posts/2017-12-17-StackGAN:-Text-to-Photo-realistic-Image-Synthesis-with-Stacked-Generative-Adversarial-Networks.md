---
layout: post
title: StackGAN:Text to Photo-realistic Image Synthesis with Stacked Generative Adversarial Networks
description: "StackGAN: Text to Photo-realistic Image Synthesis with Stacked Generative Adversarial Networks"
tags: [deeplearning]
category: deeplearning
imagefeature: cover6.jpg
comments: true
share: true
mathjax: true
---

从文本描述中生成高质量的图片在计算机视觉领域是一个很有挑战性的问题。在本文中，作者利用Stacked Generative Adversarial Networks(StackGAN)根据图片的文本描述去生成256*256图片。Stage-I GAN根据图片的描述获取图片的形状和颜色，Stage-II GAN将Stage-I的输出和图片的描述作为输入，生成high-resolution的图片。为了提高生成图片多样性，作者提出了新的Conditioning Augmentation技术。

#### 1.网络架构
![Stack_GAN](/images/gans/StackGAN.png)
**<center>图一　网络架构</center>**

##### 1.1 Conditioning Augmentation

正如上图中，文本描述ｔ首先被编码(encode)为embedding <a href="https://www.codecogs.com/eqnedit.php?latex=\varphi&space;_{t}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\varphi&space;_{t}" title="\varphi _{t}" /></a>,但是文本的latent space通常是高纬的。由于有限的文本数据，造成在latent data manifold上的不连续，这将对生成网络的学习造成影响。为了解决这个问题，作者提出了Conditioning Augmentation技术来产生更多的文本描述。从独立的高斯分布中  

![StackGan_equation1](/images/gans/StackGAN_equation.png)

随机的sample隐含的变量<a href="https://www.codecogs.com/eqnedit.php?latex=\hat{c}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{c}" title="\hat{c}" /></a>, 其中均值<a href="https://www.codecogs.com/eqnedit.php?latex=\mu&space;\left&space;(&space;\varphi&space;_{t}&space;\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mu&space;\left&space;(&space;\varphi&space;_{t}&space;\right&space;)" title="\mu \left ( \varphi _{t} \right )" /></a>和对角的协方差矩阵<a href="https://www.codecogs.com/eqnedit.php?latex=\sum&space;\left&space;(&space;\varphi&space;_{t}&space;\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum&space;\left&space;(&space;\varphi&space;_{t}&space;\right&space;)" title="\sum \left ( \varphi _{t} \right )" /></a>都是<a href="https://www.codecogs.com/eqnedit.php?latex=\varphi&space;_{t}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\varphi&space;_{t}" title="\varphi _{t}" /></a>的函数。通过这样的技术，能够产生更多的training pairs。为了避免overfitting,在目标函数里面加入了下面的正则化项:

 ![StackGan_equation1](/images/gans/StackGAN_equation1.png)

 这是标准正态分布和条件分布之间的ＫＬ散度。

#### 1.2 Stage-I GAN
文本描述embedding <a href="https://www.codecogs.com/eqnedit.php?latex=\varphi&space;_{t}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\varphi&space;_{t}" title="\varphi _{t}" /></a>作为一个全连接层的输入得到<a href="https://www.codecogs.com/eqnedit.php?latex=\mu&space;_{0}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mu&space;_{0}" title="\mu _{0}" /></a>和<a href="https://www.codecogs.com/eqnedit.php?latex=\delta&space;_{0}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sigma &space;_{0}" title="\delta _{0}" /></a>(<a href="https://www.codecogs.com/eqnedit.php?latex=\delta&space;_{0}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sigma &space;_{0}" title="\delta _{0}" /></a>为<a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma_{0}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma_{0}" title="\Sigma_{0}" /></a>对角线的元素)，<a href="https://www.codecogs.com/eqnedit.php?latex=\hat{c_{0}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{c_{0}}" title="\hat{c_{0}}" /></a>从高斯分布采样得到。<a href="https://www.codecogs.com/eqnedit.php?latex=N_{g}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?N_{g}" title="N_{g}" /></a>的<a href="https://www.codecogs.com/eqnedit.php?latex=\hat{c_{0}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{c_{0}}" title="\hat{c_{0}}" /></a>从下面的公式获得:

![StackGan_equation3](/images/gans/StackGAN_equation3.png)

其中<a href="https://www.codecogs.com/eqnedit.php?latex=\epsilon&space;\sim&space;N\left&space;(&space;0,I&space;\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\epsilon&space;\sim&space;N\left&space;(&space;0,I&space;\right&space;)" title="\epsilon \sim N\left ( 0,I \right )" /></a>,然后<a href="https://www.codecogs.com/eqnedit.php?latex=\hat{c_{0}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{c_{0}}" title="\hat{c_{0}}" /></a>和<a href="https://www.codecogs.com/eqnedit.php?latex=N_{z}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?N_{z}" title="N_{z}" /></a>的向量作为<a href="https://www.codecogs.com/eqnedit.php?latex=G_{0}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?G_{0}" title="G_{0}" /></a>的输入，生成<a href="https://www.codecogs.com/eqnedit.php?latex=W_{0}\times&space;H_{0}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?W_{0}\times&space;H_{0}" title="W_{0}\times H_{0}" /></a>的图片。  
对于判别网络\\( D_{0}\\),文本描述embedding\\(\varphi_{t}\\)首先被压缩为\\(N_{d}\\)维的向量，然后复制为\\(M_{d} \times M_{d} \times N_{d}\\)的tensor。同时图片通过一系列的down-sampling块形成\\(M_{d} \times M_{d}\\)大小。图片的特征map和文本的tensor通过channel维度进行连接，最终输入到网络中去得到分数。

#### 1.3 Stage-II GAN
由Stage-I GAN生成的图片通常不够生动(vivid),文本描述中的一些细节可能会被忽视。Stage-II GAN在Stage-I GAN生成的low-resolution的图片基础之上生成Photo-realistic的图片。  
与Stage-I GAN相同，\\( \varphi_{t}\\)被用来生成\\(N_{g}\\)维的向量\\(\hat{c}\\)。向量\\(\hat{c}\\)被复制为\\(M_{g}\times M_{g}\times N_{g}\\)的tensor。\\(s_{0}=G_{0}(z,\hat{c})\\)通过down-sampling到\\({M_{g} \times M_{g}}\\)大小。图片特征和文本特征通过channel维度进行连接后输入到几个残差块，然后经过一系列的up-sampling层最终生成W x H的图片。　　
对于判别网络，为了更好的在图片和文本描述之间对齐，作者使用了matching-aware的判别网络。在训练的过程中，判别网络将真实图片和对应的描述作为正样本。

#### 2. 优化
##### 2.1 Stage-I GAN
 不像一般的GAN直接生成high-resolution图片，Stage-I GAN主要是生成图片的形状和颜色信息。设随机的生成的向量为Z。则对应的Stage-I 最大化<a href="https://www.codecogs.com/eqnedit.php?latex=L_{D_{0}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?L_{D_{0}}" title="L_{D_{0}}" /></a>, 最小化 <a href="https://www.codecogs.com/eqnedit.php?latex=L_{G_{0}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?L_{G_{0}}" title="L_{G_{0}}" /></a>:

  ![StackGan_equation2](/images/gans/StackGAN_equation2.png)

其中<a href="https://www.codecogs.com/eqnedit.php?latex=I_{0}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?I_{0}" title="I_{0}" /></a>为真实图片，ｔ为文本描述的embedding,<a href="https://www.codecogs.com/eqnedit.php?latex=p_{data}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p_{data}" title="p_{data}" /></a>为真正的数据分布。在实验中，作者设置<a href="https://www.codecogs.com/eqnedit.php?latex=\lambda" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\lambda" title="\lambda" /></a>为１.

##### 2.2 Stage-II GAN
与Stage-I GAN不同，在这里不用使用随机noise向量，而是利用Stage-I GAN的输出\\( s_{0}\\)作为输入，损失函数为:

![StackGan_equation4](/images/gans/StackGAN_equation4.png)　
#### ３． 总结
作者提出了StackGAN,并且利用了Conditioning Augmentation技术合成了Photo-realistic的图片。与以往的方法相比，作者的方法生成了higher resolution的图片。

#### 参考
[StackGAN: Text to Photo-realistic Image Synthesis with Stacked Generative Adversarial Networks](https://arxiv.org/abs/1612.03242)
