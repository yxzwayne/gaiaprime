Question:
Temporal-Difference updates and Monte Carlo evaluation are not in conflict with each other. For instance, at a given state, we can always choose to do a Monte Carlo simulation of a trajectory from the state, and then instead of waiting to collect more trajectories from the same state, do dynamic averaging on the estimation of the state value. Do you think that's doable? If so roughly describe how you would do it in that way.

Answer: 
Yes, I think it's doable. we can perform a dynamic averaging on the estimation of state values during the simulation of trajectories. I would first calculate the temporal difference update for each state in the trajectory and then update the value of the state based on this new information.

Here's how you could roughly implement it:

1. Start with a policy $\pi$ and an initial estimate for the value function $V^{\pi}(s)$.
2. Begin a simulation, selecting actions according to the policy $\pi$.
3. At each state $s$, calculate the temporal difference update using the current estimate of the state value: $$ \delta_t = R_s(k) + \gamma V^{\pi}(s') - Q^{\pi}(s, a) $$
4. Perform dynamic averaging by updating the estimation of the state value $V^{\pi}(s)$ with the temporal difference update $\delta_t$ and the learning rate $lpha$: $$ V^{\pi}(s) \leftarrow V^{\pi}(s) + lpha 