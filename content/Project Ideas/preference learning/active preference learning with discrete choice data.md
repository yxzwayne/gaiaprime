---
tags:
  - machine-learning
  - agent
  - preference-learning
---
Active Preference Learning with Discrete Choice Data 
- Aiming for both low loss and low trial: zero-shot spirit in making inference;
- Recommendation system oriented;  

Maximizes expected value of improvement at each query without accurately modeling the entire valuation surfaces;
- Problem: space of choice is infinite
- Exploration issue: not enough compute;

# Two important insights
1. The perceptual objective function is simply unknown.
	1. Fortunately, however, it is fairly easy to judge the quality of a walk — in fact, it is trivial and almost instantaneous
2. It is not necessary to accurately model the entire objective function.
  

# Content and Notes   

> "where the desired end result is identifiable by the user, but parameters must be tuned in a tedious trial-and- error process"
> 
> "the observation that humans often seem to be forming a mental model of the objective function"
> 
- Scalable feedback loop. Not necessarily IDA (iterative distillation and amplification);
- Some tasks human are hard to do but easy to evaluate;
- In RecSys, Feedback is immediately constructed from user **point** interaction (implying low engagement, nodding to the spirit in abstract)
- Optimize towards approximating human preference or judgment for "cognitive processes and sensory perceptions"
- Each human has a function to classify animations into R/UR (real/unreal)
- Treat human preference and internals models as hidden prior, considering sampling methods haven’t taken advantages of strengths of GPU, it’s no wonder we resort to neural networks instead of statistic based methods
- Both are data driven tho? sure, data driven at this age doesn’t mean shit
- The reason sampling methods like MCMC couldn’t work is because MCMC deals with continuous random variable and this paper concerns discrete data;
- MCMC can deal with discrete data;


> The optimization model is less accurate overall, but fits the area of the maximum very well" from the paper "Active preference learning with discrete choice data
> 
- This is saying that the model may not accurately reflect all our preferences, but it does well on the preferences that matters (not decided by us, but the model when it was learning.
- Implications: if this works, can we use it as a proxy to model not human preference but nature preferences in problem spaces like protein DNA mutations

  

> "It is our thesis that the process of tweaking parameters to find a result that looks “right” is akin to sampling a perceptual objective function, and that twiddling the parameters to find the best result is, in essence, optimization"

Intuitively, RLHF is the automated process and is also more robust. 
* whether it is actually robust is an open question, but ChatGPT more or less proves it
* at the very least, RLHF with PPO is a scalable way of doing another kind of optimization following similar spirits of parameter twiddling: it just trains the parameter with feedbacks



If you wanna rate chatGPT AI on a scale, the problem is the numbers don't mean anything because one user varies from other;

Pointwise doesn't concern with scales,

the other thing is that if we have a racist response, the human annotator will be hard to produce a new answer

current architcture: whatever runs fast on gpu

current setup: 
RLHF, the reason they do PPO and RL is they have strong software on that one;
