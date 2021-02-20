# #30daysoftechreading

Day 23/30

Quote of the day:

I was scrolling through my LinkedIn today and I came across a term Graph Neural Network(GNN). I immediately googled about this interesting term which I never heard of before. To explore more about it chose to read "A Gentle Introduction to Graph Neural Networks (Basics, DeepWalk, and GraphSage)".

Graph Neural Network (GNN) has recently gained increasing popularity in various domains, including social network, knowledge graph, recommender system, and even life science. The power of GNN in modeling the dependencies between nodes in a graph enables the breakthrough in the research area related to graph analysis. This article aims to introduce the basics of Graph Neural Network and two more advanced algorithms, DeepWalk and GraphSage.

What is a Graph?

A graph is a data structure consisting of two components, vertices and edges. A graph G can be well described by the set of vertices V and edges E it contains. Edges can be either directed or undirected, depending on whether there exist directional dependencies between vertices.

G= (V,E)

Graph Neural Network
Graph Neural Network is a type of Neural Network which directly operates on the Graph structure. A typical application of GNN is node classification. Essentially, every node in the graph is associated with a label, and we want to predict the label of the nodes without ground-truth. The first proposal of GNN and thus often regarded as the original GNN.

In the node classification problem setup, each node v is characterized by its feature x_v and associated with a ground-truth label t_v. Given a partially labeled graph G, the goal is to leverage these labeled nodes to predict the labels of the unlabeled. It learns to represent each node with a d dimensional vector (state) h_v which contains the information of its neighborhood.

![alt text](https://miro.medium.com/max/750/1*p6t0CmhJgR4R_DakoagdzQ.png)


where x_co[v] denotes the features of the edges connecting with v, h_ne[v] denotes the embedding of the neighboring nodes of v, and x_ne[v] denotes the features of the neighboring nodes of v. The function f is the transition function that projects these inputs onto a d-dimensional space. Since we are seeking a unique solution for h_v, we can apply Banach fixed point theorem and rewrite the above equation as an iteratively update process. Such operation is often referred to as message passing or neighborhood aggregation.

![alt text](https://miro.medium.com/max/435/1*8hFb-3_AEkY7QRj0DOzgxg.png)

H and X denote the concatenation of all the h and x, respectively.
The output of the GNN is computed by passing the state h_v as well as the feature x_v to an output function g.


![alt text](https://miro.medium.com/max/360/1*4Yp_AB30dh5prZ2jYLyv3g.png)

Both f and g here can be interpreted as feed-forward fully-connected Neural Networks. The L1 loss can be straightforwardly formulated as the following:


![alt text](https://miro.medium.com/max/468/1*eDxF6Mblk_O9a_f4us7r6w.png)

However, there are three main limitations with this original proposal of GNN pointed out by this paper:
1. If the assumption of “fixed point” is relaxed, it is possible to leverage Multi-layer Perceptron to learn a more stable representation, and removing the iterative update process. This is because, in the original proposal, different iterations use the same parameters of the transition function f, while the different parameters in different layers of MLP allow for hierarchical feature extraction.
2. It cannot process edge information (e.g. different edges in a knowledge graph may indicate different relationship between nodes)
3. Fixed point can discourage the diversification of node distribution, and thus may not be suitable for learning to represent nodes.


DeepWalk
DeepWalk is the first algorithm proposing node embedding learned in an unsupervised manner. It highly resembles word embedding in terms of the training process. The motivation is that the distribution of both nodes in a graph and words in a corpus follow a power law.


Refer to the article for details about DeepWalk.

The main issue with DeepWalk is that it lacks the ability of generalization. Whenever a new node comes in, it has to re-train the model in order to represent this node (transductive). Thus, such GNN is not suitable for dynamic graphs where the nodes in the graphs are ever-changing.


GraphSage
GraphSage provides a solution to address the aforementioned problem, learning the embedding for each node in an inductive way. Specifically, each node is represented by the aggregation of its neighborhood. Thus, even if a new node unseen during training time appears in the graph, it can still be properly represented by its neighboring nodes. 

Refer to the article for details about GraphSage.

GraphSage enables representable embedding to be generated for unseen nodes by aggregating its nearby nodes. It allows node embedding to be applied to domains involving dynamic graph, where the structure of the graph is ever-changing. Pinterest, for example, has adopted an extended version of GraphSage, PinSage, as the core of their content discovery system.
