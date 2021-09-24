## Inductive Representation Learning on Temporal Graphs

2020 ICLR conference

### Introduction

- 任务定义
- 研究历史
- 主流方法
- 数据集
- SOTA性能
- 存在问题

### Motivation

- 现实中图在不断地变化与更新中，不断有新的节点、关系加入，原有图的拓扑结构在不断变化
- 希望获得的图嵌入向量能够捕捉到图的动态信息，例如变化的拓扑结构
- 

### Proposed Methods

- Temporal Graph Attention， 借鉴Self Attention的思想，实现一个与时间相关的aggregate function，用于在图中依据相邻节点更新自己
  - 创新点：原有的self attention依据position embedding来对相对关系进行建模，在图中中心点与邻居的距离都是直接相连，难以沿用position embedding，paper中则改用time来建模节点之间的相对关系，纪录

### Experiment

### Conclusion









