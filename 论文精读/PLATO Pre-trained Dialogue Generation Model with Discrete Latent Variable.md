## PLATO: Pre-trained Dialogue Generation Model with Discrete Latent Variable

ACL 2020

dialogue agent 论文精读

### Introduction

- 应用方向：chit-chat、QA、kowledge grounded dialogues
- 当前对话系统存在的挑战：
  - 实际应用的数据（小领域、task specific）分布与预训练的general text 差异太大
  - 生成时与预训练时采用的方法不同（例如BERT，预训练Bi-directional，生成Uni-directional）
  - One-to-many，在对话中同一个上文可以通过多种下文进行回

### Motivation

- Use latent variable to handle one-to-many situation
- 使用二次预训练方法来解决训练数据分布差异大的问题

### Proposed Methods

![image-20210925152702568](C:\Users\yeeeqichen\AppData\Roaming\Typora\typora-user-images\image-20210925152702568.png)

- framework：
  - further pre-train，消除预训练和 fine tune 时的数据差异过大问题，用与下游任务相关的无监督数据进一步预训练模型
  - 结合Uni-direction 和 Bi-direction
  - 使用Discreate latent variable来应对one-to-many 问题

- 三部分Loss
  - Relation Selective Loss：判别response和context是否匹配，帮助模型在生成response时作判别
  - NLL Loss：监督生成的response
  - BOW Loss：discard the order of geenrated sequence，训练Latent Varable全局地学习response中的信息
- 在Embedding中加入role和turn信息，帮助建模对话情景

### Experiment

- 使用的数据集：
  - Persona-Chat
  - Daily Dialog
  - DSTC7-AVSD
- baseline：
  - Seq2Seq
  - LIC
  - iVAE
