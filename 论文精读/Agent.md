## A Generalized Training Approach for Multiagent Learning

ICLR 2020 oral



### 问题设定

如何设计实现与大型系统交互（interact in large-scale system）的智能agent？新的研究方向：MARL，multi-agent reinforcement learning，多个智能体同时在同一个环境中学习（对比单智能体）

### 研究背景

过往的研究较多集中于受限场景（restricted setting）当中，例如零和（zero-sum），双人（two-player）等；使用的方法一般基于博弈论，例如Iterative Best Response Computation、Self Play、evolution-based training等，这些方法的一个共性在于都是迭代地去训练不断增大的策略集（player policies），利用启发式的打分（heuristic skill rating）或者纳什均衡。一个重要算法：Policy-Space Response Oracles

### PSRO

是对Double Oracle Algorithm进行的泛化，迭代训练。主要思想就是构建一个meta-game，由agent之间的对抗上升到population of agents 之间的对抗（2-player的话就可以用一个矩阵的形式表示，每个元素表示两个agent的模拟对战结果），然后基于当前的meta-game中的policy分布，为每个agent生成一个新的policy（例如纳什均衡），将这个新的policy加入到population当中，继续下一轮训练

“Given a game (e.g., poker), PSRO constructs a higherlevel meta-game by simulating outcomes for all match-ups of a population of players’ policies. It then trains new policies for each player (via an oracle) against a distribution over the existing meta-game policies (typically an approximate Nash equilibrium, obtained via a meta-solver1), appends these new policies to the meta-game population, and iterates."

### 文章的出发点

之前的PSRO应用主要基于纳什均衡，但是这样子的泛化性和可拓展性（scalability）不强：

- Nash Equilibria are intractable to compute
- Approximate Nash Equilibria is also intractable to compute
- 即使在某些条件下能计算了，也可能遭受Selection Problem

Key limitations: The reliance of PSRO on the Nash Equilibrium when the population grows

使用 Alpha-Rank 来替代纳什均衡作为meta-solvers（我猜meta-solver就是oracle的意思把）

### 研究的必要性

”Given that the formal study of PSRO has only been conducted under the restricted settings determined by the limitations of Nash equilibria, establishing its theoretical and empirical behaviors under alternative meta-solvers remains an important and open research problem.“

### 文章的主要贡献

- 在多种情境设定下测试了使用Alpha-Rank的有效性
- 在特定的几类对抗中建立了纳什均衡和Alpha-Rank的联系
- 

### Proposed Method



### Experiments





 

