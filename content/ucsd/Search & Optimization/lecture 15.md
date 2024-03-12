Beginning with the question: 
> what do we do after collecting some rewards?

in policy evaluation, with a fixed policy, how do we dynamically learn the subsequent policies and states.
From bellman, we know that our value function is always concerning with current state and the best possible next states. 
the problem is that now, we have one transition s -> s' with a probability we have no idea what, out of all possible s's.
Question:
- can we still use one sample of the expectation of the thing to update the s'
Intuitively, we want the learnign rate to descrease so we can focus less on the future and more on the average of history we have.

this guy named melody peijing mou keeps checking his own site lol

After going through Q learning:
imagine if we have the trajectory starting from one state S, what do we do?

Q-learning, repeat at each state S that:
- compute an action wrt eps-greedy,
- get the next state s' from the environment (MDP), which is not in our control,
- update Q(s,a) according to the expectation of R(s) + discount • max_a' Q(s',a')
- (in deep RL, fit a q-network f(s,q))
