# Background: Kaplan et al. 
Performance has a power-law relationship with each of the three scale factors _N_, _D_, _C_ when not bottlenecked by the other two, with trends spanning more than six orders of magnitude.
The power law states that the number of parameters in a neural language model, $N$, scales with the amount of computation, $C$, as $N \sim C^b$, where $b$ is a scaling exponent. 
- This means that as the amount of computation $C$ increases, the number of parameters in the model $N$ increases at a rate that is determined by the scaling exponent.
![[Screenshot 2023-01-25 at 2.50.28 PM.png]]

## Summary of Scaling Laws:
1.  For models with a limited number of parameters, trained to convergence on sufficiently large datasets: $$L(N) = (N_c/N)^{αN}\ ;\ α_N ∼ 0.076, N_c ∼ 8.8\ ×\ 10^{13}\ 	ext{(non-embedding parameters)}$$
2. For large models ($N$) trained with a limited dataset ($D$) with early stopping: $$L(D) = (D_c/D)^{lpha_D};\ lpha_D \sim 0.095, D_c \sim 5.4 	imes 10^{13}\ 	ext{(tokens)}$$
3. Limited compute ($C$), sufficient dataset ($D$), optimal model size ($N$) and batch size ($B$): $$L(C_{min}) = (C_c^{min}/C_{min})^{lpha_C^{min}};\ lpha_C^{min} \sim 0.050, C_c^{min} \sim 3.1 	imes 10^8\ \ 	ext{(PF-days)}$$
## Proposed $L(N,D)$ Equation
$$L(N,D) = rac{N_c}{N}^rac{lpha_N}{lpha_D}+rac{D_c}{D}$$
using three principles:  
1. Changes in vocabulary size or tokenization are expected to rescale the loss by an overall factor. The parameterization of $L(N, D)$ (and all models of the loss) must naturally allow for such a rescaling. 
2. Fixing $D$ and sending $N → ∞$, the overall loss should approach $L(D)$. Conversely, fixing $N$ and sending $D → ∞$ the loss must approach $L(N)$.  
3. $L(N, D)$ should be analytic at $D = \infty$, so that it has a series expansion in $1/D$ with integer powers.

Notably, In section 4.1, the paper writes "... with fixed finite D, we also do not expect any model to be capable of approaching the best possible loss. Similarly, a model with **fixed size will be capacity-limited**. These considerations motivate our second principle."

What was important? Kaplan et al. fixed the number of training tokens (or dataset size, $D$). This assumption prevented them from going further in optimizing the training of language models. 

Power Laws:
$$N(C_{min}) \propto (C_{min})^{0.73}$$
$$D \propto N^{0.74} \propto C^{0.54}$$

---


# DeepMind, Gopher and Chinchilla

We live in a world of finite stuff: resource is finite, human-generated data is finite, computational budget, at a certain time, is finite!

We want to use the computational budget, power, etc. as efficient as possible; this is not the spirit under Kaplan et al., which encouraged larger models and ignored other variables.

The Chinchilla paper investigated the optimal model and dataset size for training a transformer language model ***under a given compute budget*** $C$;
- recall that Kaplan et al. fixed data size $D$ (the number of tokens)

## Common Ground between Chinchilla and Kaplan
Large models should not be trained to their lowest possible loss to be compute optimal;

## Chinchilla Divergence
Large models **should be trained for many more training tokens** than recommended by Kaplan et al. 
- Specifically, given a 10× increase computational budget, Kaplan ea. suggests that the size of the model size should increase 5.5× while the number of training tokens should only increase 1.8×. 
- Instead, DeepMind finds that **model size** $N$ and the number of **training tokens** $D$ should be scaled in **equal** proportions.
- Visual Compare:
	- Kaplan et al.: budget: 10×, model size: 5.5×, data (token): 1.8×
	- Chinchilla: budget: 10×, model size: 5.5×, data (token): 5.5×

## Experiment
- Training **400 language models** ranging from 70M to 10 billion parameters ($N$) on 5 to 500 billion tokens ($D$);
	- Found that for compute-optimal training, the **model size  $N$ and the training dataset size $D$ should be scaled equally**
	- For every doubling of model size, the training dataset size should also be doubled;

- Test: by training **Chinchilla**, a more compute-optimal model, using the same compute budget as Gopher but with **70B** parameters and 4x more data;
	- The 70B size was determined by using the experiment result (loss) and a set of newly derived power-laws to determine that Gopher didn't need to be **280B** in parameter size, but rather chose 70B from the range of parameters acquired from experiment;
- For the same compute budget $C$, a more optimal model should be 4 times smaller but trained on 4 times more tokens.

## Conclusion
1. Transformer-based language models were significantly undertrained prior to this research, a consequence of following the model-size scaling hypothesis while forgoing other routes;
	1. How undertrained?
2. Data size is equally important as model size (parameters);

### Spin-offs

Chinchilla (**70B**) outperforms Gopher(**280B**), GPT-3 (**175B**), Jurassic-1 (**178B**), and Megatron-Turing NLG (**530B**) on downstream evaluation tasks;
- As a highlight, Chinchilla reaches an average accuracy of 67.5% on the MMLU benchmark, over a **7%** improvement over Gopher.

As for why 7% over Gopher is important:
- In December 2021, DeepMind published **Gopher**, a **280 billion** parameters transformer language model which outperforms **GPT-3** (175B) (May 2020) on Massive Multitask Language Understanding (MMLU) benchmark on the following categories ![[Screenshot 2023-01-24 at 4.53.06 PM.png]]
- The **Gopher paper** investigated the strengths and weaknesses of the different-sized models and reached the findings that: 
	- increasing the scale of a model continues to boost performance in areas like reading comprehension, fact-checking, and the identification of toxic language. 
	- model scale does not significantly improve results — for instance, in logical reasoning and common-sense tasks.


---


# Technical Details:

Question: Given a fixed FLOPs budget, how should one trade-off model size and the number of training tokens? 

The team models the final pre-training loss $L(N,D)$ as a function of the number of model parameters $𝑁$, and the number of seen training tokens, 𝐷.
Since the computational budget 𝐶 is a deterministic function FLOPs(𝑁, 𝐷) of $N$ and $D$, we are interested in:

**Minimizing 𝐿 under the constraint $FLOPs(N,D)$ = 𝐶:**
$$N_{opt}(C), D_{opt}(C) = argmin L(N,D)$$ where $N_{opt}(C)$ and $D_{opt}(C)$ are functions describing the optimal allocation of budget $C$.






## Three Approaches

Each approach obtains a relationship between model size $N$ and data size $D$ denoted as $$N_{opt} \propto C^lpha\ 	ext{ and } D_{opt} \propto C^b$$where $N$ is model size, $C$ computation and $D$ data size. These relationships are the foundation of the paper's findings and conclusions.
- $a$ and $b$ are the power variables in the power-law relationship;

### **Approach 1**
Fix the model sizes ($N$) and vary the number of training tokens ($D$); 
- trained a fixed family of models, 70M - 10B parameters, 4 different training sequences (different number of tokens $D$) 
- Extract an estimate of the **minimum loss** for a **given FLOPs**
- Doing this allowed the team to create a mapping from **FLOPs** $C$ to $N$ and $D$, the most efficient choice of model size and number of training tokens
- Finds that 𝑎 = 0.50 and 𝑏 = 0.50
- Center graph: (optimal) model size, Right: (optimal) data size![[Screenshot 2023-01-24 at 8.46.05 PM.png]]
- <span style="color:red">Once the team obtained the center and right graph, they retro-fitted Gopher's compute cost in FLOPs and determined how big Gopher could have been.</span>


### **Approach 2**
Vary the model size $N$ for a set of 9 FLOPs $C$, and consider the final training loss for each point;
- Allowed the authors to directly answer the question: For a **given FLOP** budget, what is the **optimal parameter count**?
- The valley pattern shown in the figure below means that for a given FLOP budget $C$, there is an optimal model to train;
	- The location of these valleys can project optimal $N$ and $D$ (number of tokens) for larger models
- This finds that $lpha$ = 0.49 and $b$ = 0.51
- Left: Estimated $N$ when min-loss is achieved | Center: $FLOPs$ and loss-optimal $N$ | Right: $FLOPs$ and loss-optimal $D$ ![[Screenshot 2023-01-24 at 8.53.41 PM.png]]
  The linear regressions at the center and right don't look strictly linear do they!

**Spin-off**
A simple visual comparison between approach 1 and 2 can be as:
- Approach 1:                      # of Params $N$ $
ightarrow$ # of tokens $D$
- Approach 2: FLOPs $C$ $
ightarrow$ # of Params $N$ $
ightarrow$ # of tokens $D$


### **Approach 3 - Parametric fitting of the loss**
Uses the data from the above 2 methods and fits a new model
- Model the final losses from experiments in Approach 1 & 2 as a **parametric function** of model parameter count and the number of seen tokens,
- Propose the equation: $$\hat{L}(N,D) = E+ rac{A}{N^lpha} + rac{B}{D^eta}$$
  Where:
	- $E$: the ideal generative process on the data distribution, should correspond to the entropy of natural text
	- $rac{A}{N^lpha}$: the fact that a perfectly trained transformer with $N$ parameters underperforms the ideal generative process
	- $rac{B}{D^eta}$: the fact that the transformer is not trained to convergence, as we only make a finite number of optimization steps on a sample of the dataset.

- To estimate the parameters of $L$, they minimize the Huber loss between the predicted and observed log loss using the L-BFGS algorithm: $$\mathop{min}_{A,B,E,lpha,eta}\ \ \sum_{	ext{Runs}\ i}Huber_\delta (\log\hat{L}(N_i,D_i) - \log L_i)$$
- (Need to get details of why Huber loss ($\delta = 10^{−3}$) is robust to outliers and thus important for good predictive performance over held-out data-points)
- Left: parametric modeling of the loss 𝐿ˆ(𝑁, 𝐷) | Right: isoFLOP slices ![[Screenshot 2023-01-24 at 9.20.52 PM.png]]
- **Understanding the left graph**: for a contour line, find the leftmost point, its $x$ coordinate is the optimal FLOP and $y$ coordinate the model size $N$
	- The two intersects on any other vertical line for a contour line is saying that 1B model performs on par with that of 40B (????)
	- Also highlighted where the Gopher compute budget $C$ is; (well, they went with 70B anyway)
- DeepMind also shows the **efficient frontier** in blue, which is a line in log-log space
	- The curve goes through each iso-loss contour at the **point with the fewest FLOPs**. 
	- This line projects the optimal model size $N$ given the Gopher FLOP budget to be **40B** parameters.
- Understanding the right graph: for a fixed training FLOP $C$, we can fit and find the optimal model size $N$;
- Approach 3 model finds 𝑎 = 0.46 and 𝑏 = 0.54

## Summary of the 3 Approaches
![[Screenshot 2023-01-25 at 2.14.17 AM.png]]
- Yielded comparable predictions for the optimal scaling;
- Suggested a near equal scaling in parameters and data with increasing compute, in contrast to previous work (Kaplan et al.) on scaling;
	- $dN/dC \sim dD/dC$
- The first and second approaches yield very similar predictions for optimal model sizes $N_{opt}$; 
- The third approach predicts even smaller models being optimal at larger compute budgets.

## Important Tables and Figures

### Estimated optimal training FLOPs and training tokens for various model sizes
![[Screenshot 2023-01-25 at 2.17.56 AM.png]]
This table shows that modern LMs are oversized;
- The "FLOPs (in *Gopher* unit)" column is the compute budget FLOPs that a model **should have been** trained with;
- The row of 67B parameters corresponds to 1 FLOPs in Gopher unit, meaning Gopher should have 67B params;


### Overlaying predictions of DeepMind's 3 approaches and that of Kaplan et al.'s
![[Screenshot 2023-01-24 at 7.49.34 PM.png]]

This figure suggests that large models, as they are currently used, should be **much smaller** and **trained for longer periods of time**. 
- Using similar amount of training resource (compute) available, you don't need that much parameters;
- also shows that the results of DeepMind's predictions were generally better, which
	- fixes FLOP budgets ($C$)
	- compares optimal number of **tokens** ($D$) against the optimal number of parameters ($N$)
### Alternative
![[Screenshot 2023-01-25 at 2.42.07 AM.png]]
This graph fixes FLOP budget and shows the optimal number of tokens $D$ and parameters $N$ as predicted by approach 1 and that predicted by Kaplan et al.
- For the amount of token they were trained on, pre-Chinchilla models were oversized!

### Current LLM Sizes and Training Tokens 
![[Screenshot 2023-01-24 at 8.28.59 PM.png]]
Chinchilla is smaller (less parameters $N$) but trained with more data $D$, and thus for much longer times;

### Small-scale comparison to Kaplan et al. (2020) - For $10^{21}$ FLOPs
Created two models under Approach 1 and Kaplan et al. to perform head-to-head comparison
- batch size 0.5M tokens
- max learning rate of $1.5 	imes 10^{-4}$ that decays by 10x
- Optimal model size $N$ according to Kaplan et al.: 4.68B
- Optimal model size $N$ according to Approach 1: 2.86B
- Results:
![[Screenshot 2023-01-25 at 2.44.06 AM.png]]
- In the left graph, if we cut off where the Kaplan et al. model ended (yellow), we can see that Kaplan et al. indeed performs better, but as soon as we continue training, DeepMind's approach 1 goes further;
- Under a fixed budget, Approach 1 performs better;

### Difference in modeling the scaling behaviors - Can skim over
1. DeepMind finds that setting the **learning rate schedule** to match the **number of training tokens** results in the best final loss regardless of model size, while Kaplan et al. (2020) uses a **fixed** number of training tokens and learning rate schedule for all models, preventing them from modeling the impact of these hyperparameters on the loss.
2. DeepMind includes models with up to **16B** parameters and observe that there is slight curvature in the FLOP-loss frontier, whereas the majority of runs in Kaplan et al. (2020) are significantly smaller. 


---


# A Nod to Chinchilla: The Bitter Lesson - 2019
Written by Richard Sutton on the computation cost of AI research;
- It is the most effective for AI research to leverage computation than other competing factors
- Most AI research has been conducted as if the computation available to the agent were constant, but over time, more computation becomes available;
- Researching to leverage human knowledge of the domain is important in the short run, but in the long run, the leveraging of computation is what matters;
- In computer chess and the game Go, initial efforts went into avoiding search by taking advantage of human knowledge, but all those efforts proved irrelevant or worse, once search was applied effectively at scale.
- In speech recognition, early competition in the 1970s, statistical methods won out over the human-knowledge-based methods;
	- What I get from this specific piece is we should care less about emulating human in AI research;
- The consistent direction in the field is towards methods that rely less on human knowledge, and use more computation, together with learning on huge training sets.

---

# Implications

Half way through, I realized that nostalgebraist was a better writer than me. So [here's the link](https://www.lesswrong.com/posts/6Fpvch8RR29qLEWNH/chinchilla-s-wild-implications)

---

# Beyond Scaling Laws

Paper at NEURIPS 2022

Power law scaling of error with respect to data suggests that many training examples are highly redundant (need to see how). Thus one should in principle be able to prune training datasets to much smaller sizes and train on the smaller pruned datasets without sacrificing performance.
- Introduces an unsupervised metric that does not require label information to determine what data to prune;
![[Screenshot 2023-01-25 at 3.39.44 AM.png]]
Graph B-D shows the test error as a function of data size $lpha_{prune}$ for different **fractions** of data $f$ and $	heta$, the uncertainty about target function

## Problem
Data pruning for the perceptron
## Predictions of Theory
- Keeping only the hardest examples should help when the initial dataset size is large, but hurt when it is small
- Data pruning by retaining a fixed fraction f of the hardest examples should yield power law scaling, with exponent equal to that of random pruning, as the initial dataset size increases
- The test error optimized over both initial data set size and fraction of data kept can trace out a Pareto optimal lower envelope that beats power law scaling of test error as a function of pruned dataset size, through more aggressive pruning at larger initial dataset size.
## Experiments
- Verified all three predictions on ResNets trained on SVHN, CIFAR-10, and ImageNet using varying amounts of initial dataset size and fractions of data kept under data pruning
## Conclusion
- The theory suggests that better than power law scaling can be achieved at larger initial dataset sizes and more aggressive pruning. The results also indicate that even better scaling can be achieved with even larger initial datasets.




# Old Implication Draft

The findings in the DeepMind's paper can be approached from another perspective.

Revisit the equation $$\hat{L}(N,D) = E+ rac{A}{N^lpha} + rac{B}{D^eta}$$
We can approach it in the way that
- The first term is a constant, the entropy of natural text the model is trained on;
- The second term only depends on model size, and the fact that the model only has N parameters, not infinitely many;
- The third term only depends on the data size, and the fact that the model only sees D training examples, not infinitely many;

The two latter corrections help get the entropy loss of a real model with finite $N$, $D$, $C$;
$$\hat{L}(N,D) = E+ rac{A}{N^lpha} + rac{B}{D^eta}$$
In the Appendix section D.2, the team found that E = 1.69, A = 406.4 and B = 410.7
Thus, the equation can be written as $$\hat{L}(N,D) = 1.69 + rac{A}{N^{0.34}} + rac{B}{D^{0.28}}$$
If we plug in the Gopher's statistics: 280B parameters and 300B tokens:
![[Screenshot 2023-01-25 at 3.12.34 AM.png]]
In terms of the impact on LM loss, increasing the model's parameter count $N$ leads to little gain on the entropy loss:
- Scale the model up to 500B params, or 1T params, or 100T params... and the most this can ever do is an 0.052 reduction in loss;
- Meanwhile, the "finite data" term is not tiny.
	- Gopher's training data size (300B) is very much not infinity, and we can go a long way by making it bigger.

In terms of loss, Chinchilla doesn't just beat Gopher, it beats _**any model**_ trained on Gopher's data, no matter how big.
See table:
![[Screenshot 2023-01-25 at 3.18.28 AM.png]]
Using this, the article plotted the predicted loss using Python:
![[Screenshot 2023-01-25 at 3.20.00 AM.png]]
Scaling losses: 
lamda 2.051865 
gpt3 2.002288 
gopher 1.993258 
mt_nlg 1.990615 
chinchilla 1.936645 
palm 1.923874

Take note that palm is a model of 540B parameters, the largest in the context of this presentation!
And:![[Screenshot 2023-01-25 at 3.24.03 AM.png]]
This graph shows that to achieve a marginal and trivial advantage over Chinchilla, palm used way more training compute;
To fix palm, we can use the prediction in 
