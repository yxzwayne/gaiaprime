```
Eventually we want to scale reward modeling to domains that are too complex for humans to evaluate directly.
```
# Two Assumptions
## Assumptions 1:
With enough model capacity and the right training algorithms we can extract the user’s intentions from data
## Assumption 2:
This means that reward modeling enables the user to train agents to solve tasks they could not solve themselves. 

---

For a complex system where human-based effort cannot effectively produce an outcome, we can provide enough observations and feedback system as a framework and let a model do the work for us.
Computational complexity theory was mentioned, I wonder what it is.
#  Section 3: Approach
(1) learning a reward function from the feedback of the user that captures their intentions
(2) training a policy with reinforcement learning to optimize the learned reward function.
Basically separating the "What" and "How"
## Recursive reward modeling
Leveraging agents trained with reward modeling on simpler tasks in more narrow domains in order to train a more capable agent in a more general domain.
-   Polynomially bounded quantifiers and evaluable formulas in polynomial time relate reward modeling to solving NP-complete problems.
-   NP-complete problems involve nondeterministic solutions verifiable in polynomial time.
-   An example problem discussed is finding a Hamiltonian cycle in a graph.
-   The analogy suggests evaluation is often easier than producing solutions, differentiating complexity classes P and NP.
-   Recursive reward modeling can encompass a broad range of tasks expressed in first-order logic with alternating quantifiers.
# Section 4: Challenges

- The efficacy of reward modeling is significantly influenced by the quality of the reward model.
- A reward model that doesn't fully encompass the objective can lead to the agent developing undesirable solutions.
- The agent's behavior is highly dependent on the reward model, leading to potential fragility.
- Scaling reward modeling to complex tasks introduces several challenges:
	- The affordability of the feedback required to learn the correct reward function.
	- The ability to learn a reward function that is robust against shifts in the state distribution.
	- The need to prevent the agent from exploiting loopholes in the reward model.
	- The prevention of unacceptable outcomes before they occur.
	- Training the agent to consistently exhibit behavior incentivized by the reward model, even when the reward model is correct.
- These challenges could potentially hinder the scaling of reward modeling.
- The remaining section discusses these challenges in more detail, though it doesn't claim to cover every possible challenge.
## 4.1
Didn't quite understand this part:
```
This suggests that aligning an agent may require more than just a large quantity of labeled data; we may also need to provide our models with the the right inductive bias.
```

# Misc Notes
How to select the context needed to distill questions? We have an external context for each step of distillation that the copy of the agent will need to retrieve information from.

# Recursive RL:
start with a system, human answers question, provided as training data as the next steps;
"Intelligence is just the same stuff scaled"
