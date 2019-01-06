---
layout: post
title: reading list
description: ""
tags: [deeplearning]
category: deeplearning
imagefeature: cover6.jpg
comments: true
share: true
math: true
---

图是一种常见的数据结构，广泛地应用于计算机以及相关领域。社交网络、分子结构、蛋白质结构以及推荐系统都能当做图来对待。本文介绍了当前深度学习在图上的应用。利用深度学习将图的结点或者子图映射为一个低维的向量，反映图的结构信息以及结点或子图的属性信息。  

本文主要介绍如何利用深度学习对图中的结点做embeeding,方法主要分为两大类:  
1. 直接embeeding的方法:典型的有DeepWalk和node2vec。
2. 非直接embeeding的方法:典型的有graph convolutional networks (GCN)和GraphSAGE。

![graphEncoding](/images/graph/graph_survey_1.png)
**<center>图一 图结点embeeding</center>**  
#### 一、方法的基本框架
所有的方法能抽象成为一个encoder-decoder框架。对于每一种方法，需要:
1. 一个endcoder:将图中结点encode为一个低维的向量。  
 $ENC:\nu\rightarrow R^{d}$
2. 结点之间真实的相似度
  $s_{g}$（类似于target）。例如可以将邻接矩阵A当做结点之间的真实相似度。
3. 一个decoder:利用encode后的低维向量计算图中结点的相似程度。  
$DEC\left ( z_{i},z_{j} \right )\approx s_{g}\left ( z_{i},z_{j}\right )$
1. loss函数。  
 $\sum_{(v_{i},v_{j})\in D)}l\left( DEC\left ( z_{i},z_{j} \right ), s_{g}\left ( z_{i},z_{j}\right )\right )$
    
   
#### 二、直接embeeding的方法
直接embeediing的方法首先随机初始化结点的embeeding,然后在训练的过程中优化embeeding。
#####  Laplacian eigenmaps方法
deconder为:  
$DEC\left ( z_{i},z_{j} \right )= \left \| z_{i}-z_{j} \right \|^{2}$  
损失函数为:  
$L= \sum_{(v_{i},v_{j})\in D)} DEC\left ( z_{i},z_{j} \right )\cdot s_{g}\left ( z_{i},z_{j}\right )$

#####  inner-product方法
decoder为:    
$DEC\left ( z_{i},z_{j} \right )= z_{i}^{T}\cdot z_{j}$  
损失函数为:  
$L= \sum_{(v_{i},v_{j})\in D)} \left \|DEC\left ( z_{i},z_{j} \right )-s_{g}\left ( z_{i},z_{j}\right ) \right \|_{2}^{2}$

##### 随机游走(random walk)的方法
随机游走的方法类似于NLP中训练词向量，通过随机游走来确定结点的上下文结点来优化embeeding。这里主要介绍下node2vec。
在图上进行随机游走有两个极端的情况，分别为BFS（广度优先）和DFS（深度优先）如图2。  
![bfs_dfs_1](/images/graph/bfs_dfs_1.png)
**<center>图2 BFS和DFS随机游走</center>**
两种不同的随机游走的方法学习到的结点embeeding有不同的表现。BFS学习到的结点具有社区属性(homophily），而DFS学习的结点embeeding具有结构平等性(structural equivalence)，具体如图3。

![bfs_dfs_2](/images/graph/bfs_dfs_2.png)
**<center>图3 DFS和BFS学习的embeeding对比 DFS(上) BFS(下)</center>**

现实中的图常常同时具有以上两种属性，node2vec在bfs和dfs基础之上设计了更加灵活的邻近结点的采样的方法，提高了结点embeeding在各种任务上的表现。  
假设随机游走的长度为$l$，$c_{i}$是这次游走的第$i$个结点，假设初始的结点$c_{0}$为$u$，则
$P(c_{i}|c_{i-1}) =\left\{\begin{matrix}
 \frac{\pi _{vx}}{Z}&if(v,x)\epsilon E \\ 
 0&otherwise 
\end{matrix}\right.$  
在上式中，$\pi_{vx}$为结点$v$到$x$未归一化的转移概率。Z是为了归一化。  
node2vec通过设置两个参数$p$和$q$引导游走的方向(如图4)，具体的:  
$\alpha _{pq}(t,x)=\left\{\begin{matrix}
 \frac{1}{p}&ifd_{tx}=0 \\ 
 1& ifd_{tx}=1\\ 
 \frac{1}{q}& ifd_{tx}=2
\end{matrix}\right.$  
$d_{tx}$表示结点$t$到结点$x$的距离。
则结点t到结点x的转移概率$\pi_{tx}=\alpha_{pq}(t,x)\cdot w_{tx}$。
![node_walk](/images/graph/node2vec_1.png)
**<center>图3 node2vec游走策略</center>**

在具体应用的时候，结合应用场景设置不同的$p$和$q$。当$p=1$和$q=1$时，node2vec就和deepWalk一样了。
在确定了具体的游走策略之后，对于每个结点都可以找到一组临近结点(相当于词向量中的词的上下文)，接下来就可以应用训练词向量的方法来训练结点的embeeding。  
具体的算法实现如下:  
![node2vec_algo](/images/graph/node2vec_2.png)
PreprocessModifiedWeights方法根据$p$和$q$预先算好两个节点之间的转移概率,方便后续使用。
在node2vec中为了减少计算量，随机游走的长度为$l$, 上下文的长度选择了$k$($k<l$), 则一次游走可以为$l-k$个结点中的每个结点生成k个上下文结点。

node2vec采取了灵活的游走的方法，在许多任务上取得了较好的效果。但是也有一定的局限性:
1. 没有参数共享。结点之间的embeeding之间没有参数共享。
2. 没有办法将结点的属性加入到结点的embeeding中。
3. 只能为已有的结点生成embeeding，当有新的结点加入时需要重新训练网络。


