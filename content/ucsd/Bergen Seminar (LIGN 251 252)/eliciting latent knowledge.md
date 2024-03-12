# How can we train this model to report its latent knowledge of off-screen events?

---
Tempering the camera to show happy human, despite the situation is not happy. A form of reward hacking.

Reward hacking3 is an effect that lets the agent get more reward than intended by exploiting loopholes in the process determining the reward. This problem is difficult because these loopholes have to be delineated from desired creative solutions like AlphaGo’s move 37.
Sources of undesired loopholes are reward gaming where the agent exploits some misspecification in the reward function, and reward tampering where the agent interferes with the process computing the reward.

---
# ELK Discussion
## Questions to answer
- A prediction model could show us a future that looks good but is actually bad. How does ELK prevent this?
	- By asking questions?
- What is the baseline training strategy for ELK?
- Why is the baseline inefficient?

## Toy scenario: the SmartVault
model-based RL
- input: stream of observations from cameras and one possible sequences of actions it can take;
- output: prediction of what the camera will show if that sequence of action is taken.
- In short, given $S$ and $a$, output $s_{i+1}$
Just by installing more cameras does not scale well. We should prepare for the worst case scenario.

Key: Avoid a world where powerful AI systems are searching for plans to fool us, and holding back critical information about the situation

If there "may be" strong incentives to build AI system that can select incomprehensible plans, there will be people building it and deploying it.

## Remedy Scene Hiding by Asking Questions about the environment
"Is what I’m seeing on camera what’s actually happening?"
- add a second head as question models
- Cannot directly train on these questions because it is hard to generate reliable training data
- How can the AI be trained to recognize and accurately report instances of sensor tampering that are not "extremely obvious" to humans?
## Counterexample to reporter training strategy
Training strategy learns a reporter that won’t report undetectable tampering.
Requirement, or expectation: the bad observation will need to be present in some form of information available to the Bayes Net nodes.
Bayes Nets:
If the prediction model is predicting that the camera will show a diamond because the robber is going to tamper with the camera, then the robber tampering must be reflected somehow in the inferred joint distribution over the nodes of this Bayes net.
## Question in class
Leon question:
Why do we construct the training environment such that human can only manipulate the 
Why other interventions are not possible here? 

---
# What are some ways to approach it?

---
# What is ARC’s research methodology?
