---
title: GNN相关博客
date: 2021-05-14 19:07:06
tags:
mathjax: true
---

本文是我学习GNN时浏览国内外博客所学习到的知识汇总，并总结成一些文章分享给大家。
# Expressive power of graph neural networks and the Weisfeiler-Lehman test（GNN的表达能力以及WL算法）
[原文链接](https://towardsdatascience.com/expressive-power-of-graph-neural-networks-and-the-weisefeiler-lehman-test-b883db3c7c49)

帝国理工教授Michael Bronstein，是我目前看到的，GNN相关的博客数量最高的作者。所以就从这位教授出发，慢慢总结GNN。

传统的神经网络能够逼近任何光滑函数，所以可以得到一个较为理想的准确率。但是对于GNN来说，在有些数据上表现优秀的算法在其他数据集上就突然拉胯（很多GNN都是这样的）。所以我们就想问了，GNN的表达能力到底有多强？

其中一个主要的挑战就是：GNN所面向的图数据同时具有连续性和离散性两种特点。连续性表现在节点与节点之间有边相连，离散性表现在节点是离散的。所以，一个基本的问题就是，GNN是否能够分辨不同的图结构？这是一个经典图论问题，就是“同构判定”，主要是判断两个图是否等价（大家可以这样想，如果你的图神经网络能够表达一个图数据，这不就说明你的神经网络学习到了这组数据的精髓了吗？换个角度，就是神经网络与图数据的同构判定问题。如果神经网络足够优秀，那实际上应该是和你的数据是同构的）。
> 同构是在数学对象之间定义的一类映射，它能揭示出在这些对象的属性或者操作之间存在的关系。若这两个数学结构之间存在同构映射，那么这两个结构叫做是同构的。一般来说，如果忽略掉同构的对象的属性或操作的具体定义，单从结构上讲，同构的对象是完全等价的

而对于图结构来说，同构就是两个图的边集与点集相等，与顺序无关。

那么如何判断两个图是否同构呢？这里就需要介绍一下Weisfeiler-Lehman test[<sup>1</sup>](#refer-anchor-1)，简称WL。简单来说，WL的中心思想就是使用中心节点和其邻居节点做哈希运算，得到的哈希值赋予中心节点，将这两个步骤迭代N次直至收敛。不过WL只是一个充分但不必要条件，有些时候会失效。如下图所示：
<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="GNN相关博客/2.jpg" width = "65%" alt=""/>
    <br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">
      Two non-isomorphic graphs on which the WL graph isomorphism test fails, as evident from the identical colouring it produces. In chemistry, these graphs represent the molecular structure of two different compounds, decalin (left) and bicyclopentyl (right). Figure adapted from [14].
  	</div>
</center>





说了这么多，我们就要说说WL和GNN之间的联系了。
**我们在文章开头时提到过，如果神经网络可以同构与一个图数据，那么这个神经网络就相当于学习到了图表示。** （当然了，上述文字中的同构并不是数学意义上那种严格的同构。我们只是希望神经网络学习到的节点分布能和被学习的图数据的节点分布近似或者相同。这里我们提到了分布，有了分布，就可以引入统计学了呀）实际上我们已经看到，WL中包含了GNN的<font color=red>“消息传递”，“信息聚合”</font>这两个最基本的概念。不过WL是0参数的单层感知。更为具体的相关工作大家可以参考原博客。
[参考1，kipf博客](http://tkipf.github.io/) 
[参考2，WL和GNN](https://archwalker.github.io/blog/2019/06/22/GNN-Theory-WL.html)

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="GNN相关博客/1.jpg" width = "65%" alt=""/>
    <br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">
      WL算法：上面两个图结构的节点分布近似，所以这两个图很可能是同构的。（事实上就是同构的，大家稍微思考一下就能够发现）
  	</div>
</center>

当然了，k-WL是一个更强的收敛，区别在于每个节点都会有k个哈希值。[<sup>2</sup>](#refer-anchor-2)

那么，我们就可以根据k-WL来构建一个多层GNN了。虽然从理论的角度出发，我们有了一个不错的模型，但是最近的研究成果[<sup>3</sup>](#refer-anchor-3)表明，先进的GNN模型实际上并不如以前的算法技术。这在机器学习中并不少见，因为理论和实践之间往往存在巨大差距。其中一个解释可能是基准本身的缺陷。但或许更为深刻的原因是,更好的表达能力不一定提供更好的概括(有时恰恰相反),此外,图同构可能无法准确的捕捉数据特征，我们后续再讨论这个问题。当然了，GNN的工作还是非常富有成效的，尤其是在还没有应用图方法的深度学习领域[<sup>4</sup>](#refer-anchor-4)。


<div id="refer-anchor-1"></div>

- [1] [B. Weisfeiler, A. Lehman, The reduction of a graph to canonical form and the algebra which appears therein (1968). Nauchno-Technicheskaya Informatsia 2(9):12–16. English translation and the original Russian version, which contains a pun in the form of an unusual Cyrillic notation (Операция „Ы“) referring to the eponymous Soviet blockbuster from three years earlier. See also a popular exposition in this blog post. Lehman is sometimes also spelled “Leman”, however, given the Germanic origin of the surname, I prefer the more accurate former variant.](https://davidbieber.com/post/2019-05-10-weisfeiler-lehman-isomorphism-test/#:~:text=The%20core%20idea%20of%20the,used%20to%20check%20for%20isomorphism.)

<div id="refer-anchor-2"></div>

- [2] [Weisfeiler-Lehman hierarchy. One direction of extending the results of Xu and Morris was using more powerful graph isomorphism tests. Proposed by László Babai, the k-WL test is a higher-order extension of the Weisfeiler-Lehman algorithm that works on k-tuples instead of individual nodes. With the exception of 1-WL and 2-WL tests that are equivalent, (k+1)-WL is strictly stronger than k-WL, for any k≥2, i.e. there exist examples of graphs on which k-WL fails and (k+1)-WL succeeds, but not vice versa. k-WL is thus a hierarchy or increasingly more powerful graph isomorphism tests, sometimes referred to as the Weisfeiler-Lehman hierarchy.There exist several variants of WL tests that have different computational and theoretical properties, and the terminology is rather confusing: readers are advised to clearly understand what exactly different authors mean by “k-WL”. Some authors, e.g. Sato and Maron, distinguish between WL and “folklore” WL (FWL) tests, which mainly differ in the colour refinement step. The k-FWL test is equivalent to (k+1)-WL. The set k-WL algorithm used by Morris is another variant that has lower memory complexity but is strictly weaker than k-WL.]()

  <div id="refer-anchor-3"></div>
- [3] [V. P. Dwivedi et al. Benchmarking graph neural networks (2020). arXiv: 2003.00982.](https://arxiv.org/abs/2003.00982)
  <div id="refer-anchor-4"></div>
- [4] [To be historically accurate, the WL formalism is not new to the machine learning community. The seminal paper of N. Shervashidze and K. M. Borgwardt, Fast subtree kernels on graphs (2009). Proc. NIPS was, to the best of my knowledge, the first to use this construction before the recent resurgence of deep neural networks and precedes the works discussed in this post by nearly a decade.]()

