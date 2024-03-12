---
title: Differentiability of Problems
date: 2024-01-17
tags:
  - optimization
---

(these thoughts on optimization is very rough. I will probably come back and refine these soon. see [some follow-up thoughts](#follow-up))

First few days of the Search and Optimization course, prof asked us this question:

> In the first several years of deep learning, there's a lot of research in many domains towards "differentiable" versions of their stuff (for instance, differentiable programming), with the hope that gradient descent is gonna solve many problems in an "AI" way by just doing that. Give some comments about this hope and make some predictions of what may work and what may not work.

I think aiming for differentiability is legitimate because the applicability of gradient based methods on top of differential objectives are intuitive. In the same spirit, its ease to reason is quite an intellect trap. 

One narrative that helped me obtain the intuition of gradient-based optimization methods is a tweet "linear transformations stretch euclidean space, ReLU folds euclidean space, neural networks are just repeated origami on high-dimensional laffy taffy." from [@jeffreycider](https://x.com/jeffreycider/status/1531738495848484864?s=20). 

It is intuitive that we can subject an arbitrary problem space under certain geometric and spatial rules; whether we can visualize these rules and the product is of no relevance to the legitimacy of the intuition, following the premise stated in the tweet. Then, we can naturally reason the transformation of the space based on the rules. Therefore, it should not be hard to imagine the universality of gradient-based methods given the premise of the existence of a landscape we can ascend or descend.

There are many researches regarding effectiveness of optimzers in learning problems, and so far, the more parameter and hyperparameters we introduce, the more effective the algorithms will be. Recently, there have been empirical work justifying the universal effectiveness of AdamW over SGD in langauge modeling, but unfortunately I forgot to take a screenshot or save the tweet to bookmark. I subconsciously accepted it as a prior to use adamw in my tinkering.

Even when a problem provides no differentiable objectives, people have found workarounds that utilize approximate objectives, or estimations, if you may, that are differentiable and analogous or provides reasonably close substitute objectives to the original ones. Score-matching and its applications have dominated the new-school energy based modeling techniques and led to the diffusion paradigm. Following these observations, I think we have not yet fully leveraged the differentiability and estimation methods in many problem spaces, and we have not yet fully capitalize on the effectiveness of gradient-based algorithms. I predict that finding reliably scalable ways to estimate non-differentiable objectives will be the seemingly low-hanging fruits that will lead to another breakthrough in general machine learning and specifically language modeling. 

Given how much effort went into reducing computations instead of accepting growth of compute as a premise, I guess the breakthrough will occur within 2-5 years.


## Follow-up

- what complex problems have people thought "nah we can't computationally solve those" and boom gradient descent hacked it?
- optimizer algorithms fascinate me mathematically. let's see how 
