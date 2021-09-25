## Inductive Representation Learning on Temporal Graphs

2020 ICLR conference

### source code: 

- https://github.com/StatsDLMathsRecomSys/Inductive-representation-learning-on-temporal-graphs

### 数据集

- Reddit dataset http://snap.stanford.edu/jodie/reddit.csv
- Wikipedia dataset http://snap.stanford.edu/jodie/wikipedia.csv

### Introduction

- 任务定义

  - learning low-dimentional vector embedding on graphs

- 存在问题

  - 如何捕捉图的动态变化信息

- 提出方向

  - temporal graph embedding

- 研究历史

  - Learning representations on temporal graphs is extremely challenging, and it is not until recently that several solutions are proposed (Nguyen et al., 2018; Li et al., 2018; Goyal et al., 2018; Trivedi et al., 2018).
  - 研究现状：
    - temporal graphs embedding： 2017- ：17000  2021-：12400
    - graph embedding： 2017- ：59100 2021-：26200


- baseline:
  - GAT
  - GraphSAGE



### Motivation

![image-20210924094157969](C:\Users\yeeeqichen\AppData\Roaming\Typora\typora-user-images\image-20210924094157969.png)

- 现实中图在不断地变化与更新中，不断有新的节点、关系加入，原有图的拓扑结构在不断变化
- 目前许多嵌入方法只关注图中的静态信息，但是图中许多结构信息是时间相关的（即随着时间变化），因此希望获得的图嵌入向量能够捕捉到图的动态信息，例如变化的拓扑结构
- 例：社交网络中节点间的关联是临时、动态变化的
- 存在问题：”For instance, models may mistakenly utilize future information for predicting past interactions during training and testing if the temporal constraints are disregarded“
- 挑战：如何对连续的时间进行建模

### Proposed Methods

![image-20210924094412531](C:\Users\yeeeqichen\AppData\Roaming\Typora\typora-user-images\image-20210924094412531.png)

- Temporal Graph Attention， 借鉴Self Attention的思想，实现一个与时间相关的aggregate function，用于在图中依据相邻节点更新自己，local aggregation operator
  - 创新点：原有的self attention依据position embedding来对相对关系进行建模，在图中中心点与邻居的距离都是直接相连，难以沿用position embedding，paper中则改用time来建模节点之间的相对关系，纪录每个节点的“交互时间”，定义了一个time encoding function
  - 时间：”nodes and edges are added, deleted or changed over time“
  - input sequence：![image-20210924104603552](C:\Users\yeeeqichen\AppData\Roaming\Typora\typora-user-images\image-20210924104603552.png)
    - 使用h_0作为query
  
- 为什么使用self attention？
  - 计算效率高
  - 可以有效地识别并利用邻居节点的有用信息
  
- Functional Time Encoding
  - 对时间间隔进行建模
  
- 通过层叠TGAT层来捕捉图中的长依赖信息

- Extendsion to Incorporate Edge Features
  - ![image-20210924110108401](C:\Users\yeeeqichen\AppData\Roaming\Typora\typora-user-images\image-20210924110108401.png)
  - 增加一个与边、时间相关的参数x，“interaction between vi and vj at time t induces the feature vector xi,j(t)”
  
- Loss:

  ![image-20210924200559844](C:\Users\yeeeqichen\AppData\Roaming\Typora\typora-user-images\image-20210924200559844.png)

  - link prediction loss，相近的节点在向量表示上倾向于相似

### Experiment

- link prediction

  ![image-20210924111723083](C:\Users\yeeeqichen\AppData\Roaming\Typora\typora-user-images\image-20210924111723083.png)

- node classification

  ![image-20210924111855542](C:\Users\yeeeqichen\AppData\Roaming\Typora\typora-user-images\image-20210924111855542.png)

- ablation study：验证time-encoding和TGAT-layer的有效性

- 是否能够复现：能
  - Reddit：
    - node classification：AUC 66.06
    - link prediction：ACC 93.27 AP 98.27
- 有没有改进的思路？

### Conclusion

- Self Attention as information aggregator
- Time encoding
- edge features

### 展望







