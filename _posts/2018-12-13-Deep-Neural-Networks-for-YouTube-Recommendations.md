---
layout: post
title: Deep Neural Networks for YouTube Recommendations
description: ""
tags: [deeplearning]
category: Recommenter System
imagefeature: cover6.jpg
comments: true
share: true
---

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
paper中YouToBe团队将深度学习应用于推荐系统。文中的推荐系统分为候选生成模型(deep candidate generation model)和排序模型(deep ranking model)。

#### YouTube在实现推荐系统时，面临3个挑战:
* 数据规模大。需要分布式学习算法和高效的服务系统。
* 新的用户数据。用户不断的上传新的内容,推荐系统需要对新的视频快速反应。
* 噪声。因为数据的稀疏性以及各种未被观测的外部因素，用户的行为难以预测。(很难获取用户实际的反馈)

#### 系统架构
![系统架构](/images/rs/youtube_rs_1.png)
*<center>图一　系统架构</center>*

候选生成网络以用户的历史访问信息作为输入从大量的内容中挑选中一小部分用户可能喜欢的内容。候选生成网络利用协同过滤的方法挑选出每个用户个性化的内容。用户之间的相似性则通过用户的看过的videos、搜索的关键词和地理位置等信息来表达。  
排序网络利用更加丰富的用户和内容的信息对每一个候选网络挑选出来的内容打分，将得分更高的网络排到更前面。  
通过候选网络加排序网络这种方式:(1)：在大规模的数据集上实现推荐算法，能给用户推荐个性化的内容 (2)：可以通过多种的候选方法去筛选用户可能喜欢的内容，更加灵活。

#### 候选生成网络
![系统架构](/images/rs/youtube_rs_2.png)
*<center>图二 候选生成网络</center>*
作者将推荐问题看成一个类别巨大(每个videos是一个类别)的多分类问题,所以问题变为用户U在时间t,观看视频


### 参考
* [chaptor 5.6 deeplearning book](http://www.deeplearningbook.org/contents/ml.html)