Yuxuan (Wayne) Zhang
A15120059
# Question 1
I consider a simple graph with five nodes: A, B, C, D, and E, where A is the start node and E is the goal node. The graph's connectivity and edge costs are as follows:
- A -> B with a cost of 1.
- A -> C with a cost of 3.
- B -> D with a cost of 1.
- C -> D with a cost of 1.
- D -> E with a cost of 2.

This setup forms a graph where there are multiple paths from A to E, with A-B-Dbeing the optimal path with a total cost of 4.

Then, I define the consistent heuristics $h$  for each node as the actual shortest path cost to the goal E:
- $h(A) = 4$ (A-B-D-E)
- $h(B) = 3$ (B-D-E)
- $h(C) = 3$ (C-D-E)
- $h(D) = 2$ (D-E)
- $h(E) = 0$

For new heuristic function $h'(s) = 2h(s)$:
- $h'(A) = 8$
- $h'(B) = 6$
- $h'(C) = 6$
- $h'(D) = 4$
- $h'(E) = 0$

It becomes inconsistent because the condition 
- $h'(n) \leq c(n, n') + h'(n')$ 
is violated between path A to B to D to E, as the transition from B to D would require $h'(B) = 6 \leq 1 + h'(D) = 5$, which is false.


# Question 2
## 2.1 Plots
![[Group 41.png]]

# 2.2
![[Screenshot 2024-02-25 at 23.42.50.png]]
From the plot, I can reason the improvement to the depth treenode optimization to be a slightly better chance to reach higher scores compared to the base implementations.

# 2.3 MDP for 2048

- States: A state $s \in S$ is a 4x4 grid where each cell can take on a value of $2^n$ where $n \in \mathbb{N}$ and $n \geq 0$, with the value 0 representing an empty cell. The total number of possible states is therefore vast, given the variety of combinations of cell values.
- Action $A$ consists of the four possible moves a player can make at any state: up, down, left, and right. 
- Transition function $P(s'|s, a)$ defines the probability of moving from state $s$ to state $s'$ after taking action $a$. In 2048, this is generally deterministic for the sliding and combining of tiles, but stochastic when considering the addition of a new tile (2 or 4) in a random empty position after each move.
- The reward $R(s, a, s')$ specifies the immediate reward received after transitioning from state $s$ to state $s'$ due to action $a$. In 2048,reward would be the value of the new tile created by combining tiles during the move, which incentivies the player to combine higher-value tiles.
- Under our framework, we can say that the objective in the MDP framework for 2048 is to find a policy $\pi^*$ that maximizes the expected cumulative reward, which in the context of the game corresponds to achieving the highest possible tile and score.
- The optimal policy $\pi^*$ is a strategy for the human players that, for every state $s$, chooses an action $a$ that maximizes the expected sum of future rewards. 

**How big is the state space?** 
Each cell on the 4x4 board can be in one of the states representing the power of two. If we assume upperbound to the power is 17, then the value is is $2^{17}$ (131,072). This case, each cell can be in one of 18 states (0, 2, 4, ..., 131,072). Thus, the total number of states is $18^{16}$ (since there are 16 cells, and each cell can be in one of 18 states).
$	ext{State Space Size} = 18^{16} pprox 3.8 	imes 10^{19}$

**How long will a single value iteration take in this MDP?**
We know the state space size and 4 possible actions, and I think the computation is constant when updating the value of one state. Then, assuming each state-action pair requires around 100 operations for the update. I also searched for the FLOPs for my laptop, which is $15.8×10^{12}$ FLOPS. Then, the time for a single iteration would be:
$$	ext{Time per iteration} = rac{3.8 	imes 10^{19} 	ext{ states} 	imes 4 	ext{ actions/state} 	imes 100 	ext{ operations}}{10^{12} 	ext{ operations/second}}$$

$$	ext{Time per iteration} = rac{1.52 	imes 10^{23} 	ext{ operations}}{10^{12} 	ext{ operations/second}} = 1.52 	imes 10^{11} 	ext{ seconds}$$

$$	ext{Time per iteration} pprox 4.82 	ext{ years}$$
# Question 3
## 3.1
I think this is true and intuitive, and I haven't figured out a satisfactory proof to myself...
## 3.2
From contraction mapping in the max norm of the Bellman Equation, we know:
$\|B(V) - B(V')\|_{\infty} \leq \gamma \|V - V'\|_{\infty}$

The theorem of Equivalence of Norms states that in finite-dimensional vector spaces, all norms are equivalent, which means there exist constants \(c_1, c_2\) (with \(0 < c_1 \leq c_2\)) such that for any vector \(x\):
$c_1\|x\|_2 \leq \|x\|_{\infty} \leq c_2\|x\|_2$

Hence, we have:
$\Rightarrow \|B(V) - B(V')\|_2 \leq rac{1}{c_1} \|B(V) - B(V')\|_{\infty}$
$\Rightarrow \|B(V) - B(V')\|_2 \leq rac{\gamma}{c_1} \|V - V'\|_{\infty}$
$\Rightarrow \|B(V) - B(V')\|_2 \leq rac{\gamma c_2}{c_1} \|V - V'\|_2$

This shows that the Bellman operator \(B\) is also a contraction
# 3.3
This is true.


# Question 4
## 4.1 GD has weaker condition than contraction mapping
The inequality condition for gradient descent (1) is weaker than the condition for contraction mappings because it only ensures that the distance between successive iterations decreases at a certain rate, not between any two arbitrary points. This means that while gradient descent will converge, it may do so at different rates depending on the starting point. This is intuitive retrospectively if we consider later improvements to optimizers that consider such trait of GD.
# 4.2 At most how many iterations?
Given:
$\|x_{k+1} - x^* \|_H \leq rac{\lambda_{\max} - \lambda_{\min}}{\lambda_{\max} + \lambda_{\min}} \|x_k - x^* \|_H$

We want to find the number of iterations \( k \) such that:

$\|x_k - x^* \|_H < arepsilon$

$\|x_k - x^* \|_H \leq \left(rac{\lambda_{\max} - \lambda_{\min}}{\lambda_{\max} + \lambda_{\min}}
ight)^k D$

Need to solve for \( k \) when this is less than \( arepsilon \):

$\left(rac{\lambda_{\max} - \lambda_{\min}}{\lambda_{\max} + \lambda_{\min}}
ight)^k D < arepsilon$

Log both sides:
$k \log\left(rac{\lambda_{\max} - \lambda_{\min}}{\lambda_{\max} + \lambda_{\min}}
ight) + \log(D) < \log(arepsilon)$

Solving for \( k \):

$k > rac{\log(arepsilon) - \log(D)}{\log\left(rac{\lambda_{\max} - \lambda_{\min}}{\lambda_{\max} + \lambda_{\min}}
ight)}$

Since the base of the logarithm is not specified, it is assumed to be the natural logarithm (base \( e \)). Thus, we can rewrite the expression for \( k \) as:

$k > rac{\log\left(rac{arepsilon}{D}
ight)}{\log\left(rac{\lambda_{\max} - \lambda_{\min}}{\lambda_{\max} + \lambda_{\min}}
ight)}$

# Question 5
## 5.1 MDP for Blackjack
- **States (s)**: The state in blackjack is defined by the player's current hand and the dealer's visible card. For example, a state could be (17, 10) where the player's hand totals 17 and the dealer's visible card is a 10.

- **Actions (a)**: The actions in blackjack are typically "hit" or "stand". "Hit" means to take another card, and "stand" means to stop taking cards.

- **Rewards (r)**: The rewards in blackjack are typically +1 for winning, 0 for a draw, and -1 for losing. The reward is given at the end of the game.

- **Transitions (T)**: The transition probabilities in blackjack are determined by the rules of the game. For example, if the player chooses to "hit", the next state will depend on the card drawn.

One trajectory can be:
1. **(s0, a0, s1, r1)**: ((17, 10), 'hit', (20, 10), 0) - The player starts with a total of 17, the dealer's visible card is a 10. The player chooses to "hit" and draws a 3, making their total 20. The game is not over yet, so the reward is 0.

# 5.2
