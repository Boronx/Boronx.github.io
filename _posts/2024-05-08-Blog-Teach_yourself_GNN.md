---
title: Teach Yourself GNN
author: Boron
date: 2024-05-08 09:34:00 +0200
categories: [Blogs, Machine Learning]
pin: False
tags: [Machine Learning, GNN, Tutorial]
image:
  path: https://images.unsplash.com/photo-1674027444485-cec3da58eef4?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=M3wzNjAwOTd8MHwxfHNlYXJjaHwxM3x8YWl8ZW58MHwwfHx8MTcxNDk5OTU0OHww&ixlib=rb-4.0.3&q=80&w=1080
  alt: Pic from Unsplash
---

# Basic Intro

FANTASTIC ONE!

- [x] #todo **[A Gentle Introduction to Graph Neural Networks (distill.pub)](https://distill.pub/2021/gnn-intro/)** #研究 ✅ 2024-05-08

```BibTex
@article{sanchez-lengeling2021a,
  author = {Sanchez-Lengeling, Benjamin and Reif, Emily and Pearce, Adam and Wiltschko, Alexander B.},
  title = {A Gentle Introduction to Graph Neural Networks},
  journal = {Distill},
  year = {2021},
  note = {https://distill.pub/2021/gnn-intro},
  doi = {10.23915/distill.00033}
}
```

## Representation

Representing a graph’s connectivity is more complicated. Perhaps the most obvious choice would be to use an adjacency matrix, since this is easily tensorisable. However, this representation has a few drawbacks.

- this leads to very sparse adjacency matrices, which are space-inefficient
- many adjacency matrices that can encode the same connectivity, and there is no guarantee that these different matrices would produce the same result in a deep neural network (that is to say, they are not permutation invariant #Graph_Neural_Networks)

One elegant and memory-efficient way of representing sparse matrices is as adjacency lists.

## Application of GNN

**A GNN is an optimizable transformation on all attributes of the graph (nodes, edges, global-context) that preserves graph symmetries (permutation invariances)**

Because a GNN does not update the connectivity of the input graph, we can describe the output graph of a GNN with the same adjacency list and the same number of feature vectors as the input graph. But, the output graph has updated embeddings, since the GNN has updated each of the node, edge and global-context representations.

How do we make predictions in any of the tasks we described above?  for each node embedding, apply a linear classifier.

you might have information in the graph stored in edges, but no information in nodes, but still need to make predictions on nodes. We need a way to collect information from edges and give them to nodes for prediction.
We can do this by **_pooling_**. Pooling proceeds in two steps:

1. For each item to be pooled, *gather* each of their embeddings and concatenate them into a matrix.
2. The gathered embeddings are then *aggregated*, usually via a sum operation.

### Passing messages between parts of the graph

We could make more sophisticated predictions by using pooling within the GNN layer, in order to make our learned embeddings aware of graph connectivity.

Message passing works in three steps:

1. For each node in the graph, *gather* all the neighboring node embeddings (or messages), which is the g𝑔 function described above.
2. Aggregate all messages via an aggregate function (like sum).
3. All pooled messages are passed through an *update function*, usually a learned neural network.

### Share message between nodes and edges in GNN layers

We could choose whether to update node embeddings before edge embeddings, or the other way around.

![[Weave_layer.png]]

> we could update in a ‘weave’ fashion where we have four updated representations that get combined into new node and edge representations: node to node (linear), edge to edge (linear), node to edge (edge layer), edge to node (node layer).

- [x] #Questions How to understand weave layer?

> ![[Weave_layer_in_Paper.png]]
> ?not sure if it is right, and it is good.
> it is node. in this fig, A is node, and P is edge. so there is only one time concatenation. so only En', no En''.

$$
\begin{aligned}
V_n' &= cat(\rho (V_n), f_{en1}(\rho(E_n)))\\
E_n' &= cat(\rho (E_n), f_{ne1}(\rho(V_n)))\\
V_n'' &= cat(\rho (V_n'),f_{en2}(\rho(E_n')))\\
E_n'' &= cat(\rho (E_n'), f_{ne2}(\rho(V_n')))\\
V_{n+1} &= f(V_n'')\\
E_{n+1} &= f(E_n'')
\end{aligned}
$$

$$
\begin{aligned}
V_n' &= \text{cat}(\rho(V_n), f_{en1}(\rho(E_n)))\\
E_n' &= \text{cat}(\rho(E_n), f_{ne1}(\rho(V_n)))\\
V_{n+1} &= f(V_n')\\
E_{n+1} &= f(E_n')
\end{aligned}
$$

### Adding global representation _Un_

> nodes that are far away from each other in the graph may never be able to efficiently transfer information to one another

One solution - virtual edges, let all nodes pass message with each other. **[computationally expensive]**
Another solution is to use global representations of the graph (or master node)
![[Pasted image 20240507123716.png]]

![[Pasted image 20240507124138.png]]

### Empirical GNN design lessons

- **Design Space for Graph Neural Networks**  
   J. You, R. Ying, J. Leskovec. 2020.

GNNs are a very parameter-efficient model type: for even a small number of parameters (3k) we can already find models with high performance.

Furthermore, the lower bound for performance decreases with four layers. This effect has been observed before, GNN with a higher number of layers will broadcast information at a higher distance and can risk having their node representations ‘diluted’ from many successive iterations

Overall we see that the more graph attributes are communicating, the better the performance of the average model. Our task is centered on global representations, so explicitly learning this attribute also tends to improve performance.
![[Pasted image 20240507135159.png]]

In this particular case, we could consider making molecular graphs more feature rich, by adding additional spatial relationships between nodes, adding edges that are not bonds, or explicit learnable relationships between subgraphs.

### Batching

**Sampling** [only when graphs are rather large]
The main idea for batching with graphs is to create **subgraphs** that preserve essential properties of the larger graph.
Sampling a graph is particularly relevant when a graph is large enough that it cannot be fit in memory. Inspiring new architectures and training strategies such as Cluster-GCN and GraphSaint. We expect graph datasets to continue growing in size in the future.

**Batching**

### Aggregation

The mean operation can be useful when nodes have a highly-variable number of neighbors or you need a normalized view of the features of a local neighborhood. The max operation can be useful when you want to highlight single salient features in local neighborhoods. Sum provides a balance between these two, by providing a snapshot of the local distribution of features, but because it is not normalized, can also highlight outliers. In practice, sum is commonly used.

# Modules

AA

## LAST

A
