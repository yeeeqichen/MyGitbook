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





### Summary （1pt）

- PSRO with Alpha-Rank: Analyzes and extends learning methods based on Policy-Spaced Response Oracles(PSRO) through the application of alpha rank.

- Based on theoretical findings showing shortcomings of using the typical best response oracle, the paper finds a necessity for a new response oracle and proposes Preference-based Best Response(PBR).

- Explore connectionss with Nash Equilibrium 

- Shown that it is possible to give theoretical guarantees for a version of PSRO driven by α-Rank in several circumstances for general-sum multi-player games.

- Multi Agents: Demonstrate empirical results extending beyond the reach of PSRO with Nash as a meta-solver by evaluating training in 3-player to 5-player game.

  

### Strengths （1pt）

- The experiments are sufficent and comprehensive. This paper not only study the theory and practice of proposed method PSRO(Alpha-Rank as meta-solver, Preference-based Bset Response), but also investigate the connection to the Nash-based PSRO methods. 

- Detailed examples of the case in which the PSRO(Alpha-Rank as meta-solver, Best Response as oracles) can't work properly. The author explain this via concrete examples, makes the illrustration easy to understand.

- The figures are simple yet sufficient, makes the paper more easy to read.

- Many supplementary information in Appendix, thoroughly explain the theroies and examples uesd in the paper. 

- This paper provides a nice balance of theoratical support and practical relevance, which should be of high impact to the RL research fields.

- The code is provided, makes it easier to reproduce the results and paves the way for future study in this field.

  

### Weakness （1pt）

- I think some terms in the paper seems to be clarified, or it would be quite hard to read for readers not familiar with this area. For example, what is the details about the oracle used in experiments? How does it work?

- What is the dependency of alpha? In the previous paper about alpha rank by Omidshafiei et al. (Nature, 2019), the authors say a lot about choosing the right value of alpha. How was alpha in this paper chosen?

  

### Detailed Comments （1pt）

- I think the Preliminaries part is too densily written and quite hard to read, it would be helpful if some figures that illerastrated the mentioned term in this section could be added.

### Figures （1pt）

- PSRO algorithms: including three steps, Complete, Solve and Expand. Given a game (e.g., poker), PSRO constructs a higherlevel meta-game by simulating outcomes for all match-ups of a population of players’ policies. It then trains new policies for each player (via an oracle) against a distribution over the existing meta-game policies and appends these new policies to the meta-game population, and iterates.

  ![image-20210927092700989](/Users/yeeeqichen/Library/Application Support/typora-user-images/image-20210927092700989.png)

- A Theory Overview in the paper. Compares different combinations of Game Type, meta-solvers and oracles, with respect to the converges to alpha-rank.

  ![image-20210927134519143](/Users/yeeeqichen/Library/Application Support/typora-user-images/image-20210927134519143.png)

- Compare different meta-solvers with setting: PSRO (meta-solvers, BR), in this experiment, BR remains fixed, the meta-solvers are chosen from {Uniform, alpha-rank, PRD, Nash, PRD(rectified), Nash(rectified)}. The NashConv scores measure the distance against Nash Equilibrium, 0 means convergence. From the figure below we can see that the alpha-rank based PSRO. This experiment demonstrate that the alpha-rank could be applied competitiveively in the two-player zero sum setting.

  ![image-20210927153922882](/Users/yeeeqichen/Library/Application Support/typora-user-images/image-20210927153922882.png)

- Multi agents (larger than 2 players) situation, demonstrate that alph-rank could be used in situations with more than 2 players, in which the Nash based methods couldn't handle.

  ![image-20210927155050871](/Users/yeeeqichen/Library/Application Support/typora-user-images/image-20210927155050871.png)

- A step by step example to explain why PSRO(with alpha rank as meta solvers and BR as oracles) will not work in some single-population case. Clear and easy to understand.

  ![image-20210927134815293](/Users/yeeeqichen/Library/Application Support/typora-user-images/image-20210927134815293.png)

  ![image-20210927134750710](/Users/yeeeqichen/Library/Application Support/typora-user-images/image-20210927134750710.png)

- The visualized game tree of two players policies. Play 1's decision nodes indicated by the blue squares, and action indicated by the blue arrows. Player 2's are likewise shown via red counterparts. With this graph, we can easily understand the game setting and the agent actions during the game. Our goal is to train agents that could take feasible actions to win other agents.

  ![image-20210927142441793](/Users/yeeeqichen/Library/Application Support/typora-user-images/image-20210927142441793.png)

  ![image-20210927142453574](/Users/yeeeqichen/Library/Application Support/typora-user-images/image-20210927142453574.png)
