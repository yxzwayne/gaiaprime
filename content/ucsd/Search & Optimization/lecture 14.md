This lecture discusses policy evaluation in the context of Markov Decision Processes (MDPs) with states, actions, rewards, and probability distributions, with a focus on the problem of evaluating a policy, given that we no longer have access to the probability distribution required for Bellman updates.

**Monte Carlo Algorithm for Policy Evaluation**

The Monte Carlo algorithm for policy evaluation is used to estimate the value function $V^{\pi}(s)$ for each state $s$ in the MDP, where $\pi$ is a policy. The idea is to take samples of trajectories and calculate the expected rewards for each state. This can be seen as an approximation of the Bellman updates.

If we have enough samples, we can estimate the value function $V^{\pi}(s)$ as follows:
$$
V^{\pi}(s) = rac{1}{|K|} \sum\limits_{k \in K} R_s(k)
$$
where $|K|$ is the size of the set $K$, and $R_s(k)$ is the reward obtained starting from state $s$ at time step $k$.

**Temporal Difference Learning**

The Monte Carlo algorithm evaluates the policy but does not optimize it. To address this, we use temporal difference learning, which modifies the Bellman equation to update values based on both current and future rewards. The resulting update rule is:
$$
V^{\pi}(s) \leftarrow V^{\pi}(s) + lpha 