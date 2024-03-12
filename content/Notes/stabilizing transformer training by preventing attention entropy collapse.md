---
title: Stabilizing transformer training by preventing attention entropy collapse
tags:
  - literature-review
  - notes
---

Authors: Shuangfei Zhai, Tatiana Likhomanenko, Etai Littwin, Dan Busbridge, Jason Ramapuram, Yizhe Zhang, Jiatao Gu, Josh Susskind
# Related Work

## Normalization and Initialization
- Transformers rely heavily on Layer Normalization (LN)
- Various LN configurations have been proposed
- Proper initialization is crucial, but training dynamics are equally important

Layer normalization (LN) is a technique that helps improve the training stability of deep neural networks by normalizing the input across the features;
- Post-LN: In Post-LN configuration, the layer normalization is applied after the residual connection in the Transformer block.
- Pre-LN: layer normalization is applied before the self-attention mechanism and the residual connection. This approach was later proposed as an alternative to Post-LN due to its improved training stability and faster convergence.

## Weight Reparameterization - may be could have provided more context;
- WeightNorm (WN) and additive weight reparameterization in ConvNets
- σReparam is a special weight reparametrization technique;
	- the first simple reparameterization technique providing competitive performance in Transformers
	- Built on top of SpectralNorm
    	- The [spectral norm](https://arxiv.org/pdf/1705.10941.pdf) of a matrix is defined as the largest singular value of that matrix, which essentially measures its largest possible stretching factor. In the context of transformer model training, applying spectral normalization helps in stabilizing the training process by ensuring that the weights of the network do not grow uncontrollably large, thus preventing the gradients from exploding. This technique is particularly useful in maintaining the balance between the different layers of the transformer, facilitating smoother and more stable convergence during training.

## Rank Collapse vs Entropy Collapse
- Rank collapse: attention output converges to a rank 1 matrix (Dong et al., 2021)
- Entropy collapse: attention matrix remains high rank and introduces high gradient norms
	- Question - does high rank matrix necessarily imply high gradient norms? 
		- Paper says so but we spent some time reasoning why;
		- vanishing gradient of the attention query and keys;
	- Discussion: attention matrix is a stochastic matrix;

---
# Attention Entropy

## Formulation
- Input sequence: $X \in \mathbb{R}^{T \times d}$ where $T$ is the number of tokens and $d$ is the token dimension.
  
- Key, query, and value matrices: 
  - $W_K, W_Q \in \mathbb{R}^{d \times n_a}$ and $W_V \in \mathbb{R}^{d \times n_v}$, where $n_a$ and $n_v$ are dimensions for the attention mechanism.
  
- Attention layer: $Att(X) = A X W_V$ where $A = \psi(a)$, $a = X W_K W_Q^{\top} X^{\top}$, and $\psi$ is the row-wise softmax function.

## Definition
- Attention entropy for row $i$ of $A$: 
  $$Ent(A_i) = -\sum_{j=1}^{T} A_{i,j} \log(A_{i,j})$$
- Average attention entropy of $A$: 
  $$Ent(A) = \frac{1}{T} \sum_{i=1}^{T} Ent(A_i)$$
- Objective: To mitigate the entropy collapse issue and ensure a gradual evolution of attention entropy throughout the training process.

Why can we define entropy in this process?
- Because the attention matrix A is a probability distribution. 
- Each row $i$ of $A$ is a probability distribution over the other tokens in the sequence
Why do we concern with the average attention entropy?
- Because we want to capture the overall focus/dispersion of the attention mechanism across the entire input sequence. 
- By taking the average entropy value of all rows in the attention matrix, we obtain a single value that reflects the overall attention entropy and gives us a way to quantify how focused or dispersed the attention is on the input.

- look up the frobenius norm with respect to the sum of all singular values;

---

## Write-up my own simplicity 

Attention entropy is a measure of the distribution of attention across tokens in a given sequence. It quantifies how focused or dispersed the attention mechanism is when processing the input sequence. For each token in the sequence, attention entropy measures the uncertainty or randomness in the attention distribution over other tokens.

To compute attention entropy, first, look at the attention matrix $A$, which is derived from the input sequence and the key matrix $K$, query matrix $Q$, and value matrix $V$. Each row of the attention matrix represents the attention distribution for a specific token in the input sequence. In other words, it tells us how much attention the token pays to other tokens in the sequence.

Next, for each row of the attention matrix, we calculate its entropy using the standard formula for entropy: multiplying the probability (attention weight) of each element in the row by the logarithm of that probability, summing these products, and then taking the negative of this sum. This process results in the entropy for each row, which represents the attention entropy for a single token in the input sequence.

Finally, we average the entropy values for all rows in the attention matrix to obtain the overall attention entropy. This average attention entropy gives us a single value that reflects the focus or dispersion of the attention mechanism across the entire input sequence. A higher entropy value indicates a more uniform distribution of attention across tokens, while a lower entropy value indicates that the attention is more focused on a smaller number of tokens.

---

# Observation

1. Attention entropy is tightly correlated with the model’s stability and convergence
	1. Small entropy bad - slow convergence or divergence;
2. Similar observations can be made if hyperparameters such as learning rate, warmup, initialization are not carefully tuned
![[Screenshot 2023-04-18 at 1.06.15 PM.png]]

![[Screenshot 2023-04-18 at 1.07.08 PM.png]]


## Proposed solution

1. change the weights W in the attention by normalizing them and learning a parameter γ This avoids the attention problem, but does it change stabillity


---

The proposed theorem, Theorem 3.1, provides a lower bound for the attention entropy. It establishes a connection between the attention entropy and the spectral norm of the product of the key and query weight matrices.

# Theorem

Let $\sigma=\left\|W_K W_Q^{\top}\right\|_2$,

$\sigma_x=\left\|X X^{\top}\right\|_2$,

$\sigma=\sigma \cdot \sigma_x$,

and $\eta= \exp \left(-\boldsymbol{\sigma} \sqrt{\frac{T}{T-1}}\right)$. 

Then it holds that:

$$ \operatorname{Ent}\left(A_i\right) \geq \log \left(1+(T-1) \eta\right)+\frac{\sigma \sqrt{T(T-1)} \eta}{1+(T-1) \eta}$$ 

when $\sigma=\left\|W_K W_Q^{\top}\right\|_2$

This represents the spectral norm of the product of the key and query matrices. 
1. The spectral norm is the largest singular value of a matrix and provides a measure of how much the matrix can scale a given vector. 
2. In the context of Transformer attention, $\sigma$ reflects the scaling property of the key-query interaction.

$$\sigma_x=\left\|X X^{\top}\right\|_2$$
This is the spectral norm of the product of the input sequence and its transpose, i.e., $\sigma_x = \|X X^{\top}\|_2$. It characterizes the scaling property of the input sequence.

$$\sigma=\sigma \cdot \sigma_x$$
* Question: are these $\sigma$ larger or smaller than 1?

This is the product of the spectral norms $\sigma$ and $\sigma_x$. It provides a measure of the combined scaling effects of the key-query interaction and the input sequence. 
- the smaller the better, because it indicates that the spectral norm of the weight matrices is smaller, which helps to prevent attention entropy collapse and improve training stability
- This is absorbed into a single parameter $\gamma$ in the $\sigma$Reparam method;

$\eta= \exp \left(-\boldsymbol{\sigma} \sqrt{\frac{T}{T-1}}\right)$
This parameter is an exponential function of the combined scaling effect $\sigma_{total}$, with an additional factor $\sqrt{\frac{T}{T-1}}$ that depends on the number of tokens, T. $\eta$ is used in the lower bound of the attention entropy, as shown in the theorem.

# $\sigma$Reparam

The $\sigma$Reparam technique is a strategy for reparameterizing the weights in a linear layer, defined as follows:
$$\widehat{W}=\frac{\gamma}{\sigma(W)} W$$
where:
- $\sigma(W) \in \mathbb{R}$ represents the **spectral norm** of $W$,
- $\gamma \in \mathbb{R}$ is a learnable parameter, initially set to 1.
Understand this:
The spectral norm of W times a scalar is equal the scalar times the previous sv, so \hat{W} = c • W and so SN(W) is $\gamma$

The author steps away from loss geometry perspective ([Chen et al. 2021a](https://arxiv.org/pdf/2106.01548.pdf)) and identify a novel empirical observation unique to the Transformer architecture.

Key aspects of $\gamma$Reparam include:
-   It separates the update rate of the spectral norm, represented as $$\Delta \sigma = \eta \frac{(\Delta W)_F}{\sigma},$$ from the influence of weight matrix dimensionality. This separation can mitigate the risk of uncontrolled spectral norm increases in large weight matrices, a common issue when employing adaptive optimization techniques.
-   $\gamma$Reparam introduces a dimensionality-independent update mechanism for a singular parameter $\gamma$, diverging from traditional weight matrix parameterization approaches.
-   Unlike methods such as SpectralNorm, which directly limit the model's representational space, $\gamma$Reparam maintains the network's representational capacity. It achieves this by promoting a unique optimization dynamic, thereby distinguishing itself from conventional normalization techniques.

-> Detour: how does Spectral Norm constrain model space?

By normalizing the weights of the neural network layers, controlling the Lipschitz constant of the model and preventing it from becoming too large. This helps reduce the risk of mode collapse, vanishing or exploding gradients, and improves the training dynamics.

The main idea behind Spectral Normalization is to divide the weights of a layer by its largest singular value, also known as the spectral norm. By doing this, the Lipschitz constant of the model is constrained, leading to a more stable and controlled training process.

1. Compute the spectral norm (σ) of a weight matrix W (the largest singular value of W) which can be efficiently approximated using the power iteration method.
2. Normalize the weight matrix W by dividing it by its spectral norm: $W_{normalized} = W / \sigma$
3. Replace the original weight matrix $W$ with the normalized one, $W_{normalized}$, in the neural network.

-   $\gamma$Reparam brings little extra overhead as the power iteration mainly consists of two matrix vector products and is only performed on the parameters rather than activations.
-   During inference, one can compute $\hat{W}$ once and freeze it, which has the same cost as a regular linear layer.

## Proposition Lower-bound


$$\sigma(\Delta) \geq \sqrt{w} \sqrt{1-\frac{1}{w^2} \sum_{i, j=1}^w \frac{n_{i, j}^2}{\mu_{i, j}^2+n_{i, j}^2}}$$

---

# Experiment 

The authors show a consistent ability to train well in Vision (fig) and language Even without all of our other tricks In the fig, they train without LN, decay, cosine\warmup LR schedule, on SGD and get good results with models known to overfit.

![exp1](figures/screenshot%202023-04-18%20at%201.33.01%20pm.png)

![exp2](figures/screenshot%202023-04-18%20at%202.06.45%20pm.png)

![exp3](figures/screenshot%202023-04-18%20at%202.08.31%20pm.png)

I read this graph as that getting rid of pre-layer-norms help further improve stability;

The following graph is the result of the experiment in which
- the author inject σReparam into post-LN and DeepNorm models,
- shows that σReparam nicely bounds attention entropy for 18L-18L and 50L-50L post-LN models;

The author also claims that this resolves the problem of vanishing gradients - what's the math process?

---
# Conclusion

## Causal relationship between entropy collapse and training instability

The authors mention that it is unclear whether there is a causal relationship between attention entropy collapse and training instability in Transformers. 
- Establishing such a connection would enable a deeper understanding of the challenges of Transformer training from the optimization perspective and potentially lead to improved techniques to address these issues.

## Complementary techniques to σReparam

While σReparam is effective in addressing entropy collapse and improving training stability, it is not a complete solution. The authors encourage the exploration and development of additional techniques that can be combined with σReparam to further enhance training stability and robustness. This may include better initialization methods, feature normalization techniques, advanced optimizers, and other design and training principles that can help improve Transformer training.

## Limitation

- No established direct causal relationship;
- σReparam is not a one-size-fits-all solution. In practice, it may still be beneficial to combine σReparam with other techniques, 
	- better initialization methods, 
	- feature normalization, 
	- and advanced optimizers
