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

#### 2018.12.04
1. 如何处理缺失值:Kuhn and Johnson(2013)
2. xgb如何处理缺失的值：对于缺失值，学习一个方向（left and right）。当有数据缺失时，默认的方向被take.
3. cart如何处理缺失值：代理split。具体是怎么实现的
4. Categorical Predictors：xgb和cart如何处理多类的问题？![ca52108b1cf0f38c7b93d3674d9b0208.png](evernotecid://1F3523CB-5AC7-452F-8BEC-B688CA484466/appyinxiangcom/16449579/ENResource/p10)
#### 2018.12.05
1. Recommendation models : collaborative filtering,content-based recommender system and hybrid recommender system based on the types of input data。
2. inductive bias:算法预测未见到的样本的假设的结合 
3. DeepMF by proposing a eXtreme deep factorization machine to jointly model the&nbsp;explicit and implicit feature interactions.Wide and deep:memorization and generalization.
4.  triangle inequality:In Euclidean geometry.
   vector x and y ![2662edd21f568cbce801f62ab7e18572.png](evernotecid://1F3523CB-5AC7-452F-8BEC-B688CA484466/appyinxiangcom/16449579/ENResource/p11)
   <span style="color:red">how dot product does not satisfy the triangle inequality of distance function？</span>
5. resilient propagation, L-BFGS
#### 2018.12.06
1. BPR loss
2. 
#### 2018.12.15
1. label smoothing:Rethinking the Inception Architecture for Computer Vision
2. perplexity: 
In information theory, perplexity is a measurement of how well a probability distribution or probability model predicts a sample.  
![perplexity](/images/note/perplexity.svg)  
https://www.quora.com/What-is-perplexity-in-NLP
#### 2018.12.16
1. tensorflow transformer实现  
   * attention bias: 对输入进行mask.将输入中为0的值mask为负无穷.  
  Bias tensor that is added to the pre-softmax multi-headed attention logits,
  which has shape [batch_size, num_heads, length, length]. The tensor is zero at
  non-padding locations, and -1e9 (negative infinity) at padding locations.
2. encoder
   * Scale embedding by the sqrt of the hidden size
   * 对Inputs的embedding也mask为0
   * 每个token的embedding加上pos_embedding
   * Multi-head attention的具体做法:  
     *  head指的是将每个embedding分为多个部分,然后分别做对每一个部分分别做self-attention。
     *  加上bias
     *  在组合为[batch_size, length, hidden_size]
3. decoder
   * attension bias: 为了防止前面的attention用到了后面的信息，对输入进行mask（用一个矩阵，对角线上面的元素全为负无穷(-1e-9),对角线下的元素全为0） 
   * 具体的attention与encoder一样，只不过attension bias不一样。
#### 2018.12.17
Representation Learning on Graphs: Methods and Applications
* **primary challenge**: represent, or encode, graph structure so that it can be easily exploited by machine learning models. 
* **traditional method**:relied on user-defined heuristics to extract features encoding structural information about a graph.(e.g., degree statistics or kernel functions)
* **deep learning**: matrix factorization-based methods, random-walk based algorithms, and graph convolutional networks. 这些方法可以分为两类:embed individual nodes as well as approaches to embed entire (sub)graphs
#### 2018.12.18
*  matrix factorization techniques
*   frobenius norm