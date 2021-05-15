---
title: GNN学习笔记
date: 2021-01-10 13:32:51
tags:
mathjax: true
---
# 吐槽
本篇笔记实际上是GSN的草稿。


# 图论的基本概念

边与两端点称为**关联的(incident)**

与同一条边关联的两端点或者与同一个顶点关联的两条边称为**相邻的(adjacent)**

两端点相同的边称为**环(loop)**

有公共起点并没有公共终点的边称为**平行边(paralled edges)**

无环并且无平行边的图称为简单图。

设G为无向图，$x \in V(G)$的顶点度(vertex degree)定义为G中与x关联边的数目，记为$d_G(x)$

1.4 导出子图和支撑子图


1.5 路和连通
图$D$(或$G$)中连接顶点$x$和y且长度为k的链W，记为

p32最后一段：割边和割点


4.3 LIMITATIONS
Though experimental results showed that GNN is a powerful architecture for modeling struc-
tural data, there are still several limitations of the vanilla GNN.
• First, it is computationally inefficient to update the hidden states of nodes iteratively to get
the fixed point. The model needs T steps of computation to approximate the fixed point.
If relaxing the assumption of the fixed point, we can design a multi-layer GNN to get a
stable representation of the node and its neighborhood.
• Second, vanilla GNN uses the same parameters in the iteration while most popular neural
networks use different parameters in different layers, which serves as a hierarchical feature
extraction method. Moreover, the update of node hidden states is a sequential process
which can benefit from the RNN kernels like GRU and LSTM.
• Third, there are also some informative features on the edges which cannot be effectively
modeled in the vanilla GNN. For example, the edges in the knowledge graph have the
type of relations and the message propagation through different edges should be differ-
ent according to their types. Besides, how to learn the hidden states of edges is also an
important problem.
22 4. VANILLAGRAPH NEURALNETWORKS
• Last, if T is pretty large, it is unsuitable to use the fixed points if we focus on the repre-
sentation of nodes instead of graphs because the distribution of representation in the fixed
point will be much more smooth in value and less informative for distinguishing each
node.