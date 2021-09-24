### Modeling Relational Data with Graph Convolutional Networks

- 任务：KRL

- GCN encoding model

- node loss + edge loss

- edge loss 计算和具体的score function有关

- negative sampling

- **模型参数与关系相关，parameter explosion**

  

### Composition-Based Multi-Relational Graph Convolutional Networks

- 任务：KRL
- 创新点：GCN，同时对entity和relation作嵌入，不再将关系建模进模型参数中，**避免参数爆炸**
- 针对正向、反向、自反三种有向边类型定义了三种信息传递矩阵
- 每个节点的信息由其直接邻居和对应关系传递累加得到
- 通过对GCN进行**叠加**，可以捕捉到知识图谱中的长依赖关系



### Iterative Entity Alignment via Joint Knowledge Embeddings

- 任务：EA

- 处理实体对齐问题，通过将实体和关系映射到一个统一的向量空间（对齐后）解决

- 定义三部分loss：KGEloss、JointLoss、IterativeLoss
  - KGEloss用于学习单个知识图谱内向量表示
  - JointLoss用于**对齐**两个向量空间
  - IterativeLoss与新加入的对齐pair（e1，e2）有关，迭代更新
    - Hard Alignment：直接更新对齐的实体向量，不够鲁棒
    
    - Soft Alignment：定义Loss，**加权更新**，降低误判带来的后果
    
      

### Graph Convolution over Pruned Dependency Trees Improves Relation Extraction

- 任务：RE

- 创新点：把dependency tree 转化为一个邻接矩阵，从而执行GCN操作

- 通过预训练模型（LSTM、Transformer等）获得word embedding，再进行GCN操作

  

### Joint Extraction of Entities and Relations Based on a Novel Tagging Scheme

- 任务：End-to-End NER + RE
- 创新点：把NER + RE建模成一个序列标注任务，同时识别实体及其对应关系




### Inductive Representation Learning on Temporal Graphs

- 任务：KRL
- 出发点：知识图谱随时间不断变化
- 创新点：引入时间变量，将embedding与时间节点相关联，借助temporal graph来学习嵌入向量表示
- 对邻居进行attention，position替换为与target的交互时间

