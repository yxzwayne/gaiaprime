I also realized that I did not apply any variational inference improvement techniques
- tempering posterior
- cold posterior


Variational inference is a specific technique within the broader framework of Bayesian inference, but not all Bayesian inference methods are variational. Let's explore this in more detail using mathematical intuition and expressions.

In Bayesian inference, we aim to compute the posterior distribution $p(	heta|x)$ of the parameters $	heta$ given the observed data $x$. This is done using Bayes' theorem:

$p(	heta|x) = rac{p(x|	heta)p(	heta)}{p(x)}$

where $p(x|	heta)$ is the likelihood, $p(	heta)$ is the prior, and $p(x)$ is the evidence or marginal likelihood.

The main challenge in Bayesian inference is that the evidence $p(x)$ is often intractable to compute, as it requires integrating over the entire parameter space:

$p(x) = \int p(x, 	heta) d	heta = \int p(x|	heta)p(	heta) d	heta$

Variational inference addresses this challenge by introducing a variational distribution $q(	heta)$ to approximate the true posterior $p(	heta|x)$. The goal is to find the optimal variational distribution $q^*(	heta)$ that minimizes the Kullback-Leibler (KL) divergence between $q(	heta)$ and $p(	heta|x)$:

$q^*(	heta) = rg\min_{q(	heta)} KL(q(	heta) || p(	heta|x))$

where the KL divergence is defined as:

$KL(q(	heta) || p(	heta|x)) = \int q(	heta) \log rac{q(	heta)}{p(	heta|x)} d	heta$

By minimizing the KL divergence, variational inference finds the best approximation to the true posterior within the family of variational distributions.

However, variational inference is just one approach to Bayesian inference. Other methods include:

1. Markov Chain Monte Carlo (MCMC) methods, such as Gibbs sampling and Metropolis-Hastings algorithm, which generate samples from the posterior distribution without explicitly computing the evidence.

2. Laplace approximation, which approximates the posterior distribution with a Gaussian distribution centered at the mode of the posterior, using a second-order Taylor expansion of the log-posterior.

3. Expectation Propagation (EP), which approximates the posterior by iteratively refining local approximations to the factors of the posterior distribution.

These methods do not rely on variational approximations and instead use different techniques to estimate or sample from the posterior distribution.

---
lmfao this is wild, p(x) is hard to compute (integrals hrrrr), and somehow we approximate p(theta|x) ?????

---
You're right, it might seem counterintuitive at first! Let me break it down further.

In Bayesian inference, our main goal is to compute the posterior distribution $p(	heta|x)$, which tells us the probability of the parameters $	heta$ given the observed data $x$. However, computing $p(	heta|x)$ directly using Bayes' theorem involves calculating the evidence $p(x)$, which is often intractable due to the high-dimensional integral.

Variational inference takes a different approach. Instead of directly computing $p(	heta|x)$, we introduce a variational distribution $q(	heta)$ that belongs to a family of distributions we can easily work with, such as Gaussian distributions. We then try to find the best $q(	heta)$ that approximates the true posterior $p(	heta|x)$ by minimizing the KL divergence between them.

Now, here's the key insight: minimizing the KL divergence between $q(	heta)$ and $p(	heta|x)$ is equivalent to maximizing the evidence lower bound (ELBO):

$ELBO(q) = \mathbb{E}_{q(	heta)}[\log p(x, 	heta)] - \mathbb{E}_{q(	heta)}[\log q(	heta)]$

The ELBO consists of two terms:

1. $\mathbb{E}_{q(	heta)}[\log p(x, 	heta)]$: This is the expected log joint probability of the data and parameters under the variational distribution. It encourages $q(	heta)$ to place its probability mass on parameter values that explain the observed data well.

2. $-\mathbb{E}_{q(	heta)}[\log q(	heta)]$: This is the negative entropy of the variational distribution. It encourages $q(	heta)$ to be as uncertain as possible, preventing it from collapsing to a single point estimate.

By maximizing the ELBO, we find the best variational distribution $q^*(	heta)$ that balances between explaining the data well and maintaining a reasonable level of uncertainty. Importantly, the ELBO does not involve the intractable evidence $p(x)$, making it easier to optimize.

So, even though directly computing $p(	heta|x)$ is difficult due to the intractable evidence $p(x)$, variational inference allows us to find a good approximation $q^*(	heta)$ by optimizing the ELBO, which depends only on the joint distribution $p(x, 	heta)$ and the variational distribution $q(	heta)$.

In practice, the ELBO is often optimized using techniques like coordinate ascent variational inference (CAVI) or stochastic variational inference (SVI), which iteratively update the variational parameters to improve the approximation.

To summarize, variational inference bypasses the difficulty of computing the intractable evidence $p(x)$ by introducing a variational distribution $q(	heta)$ and optimizing the ELBO to find the best approximation to the true posterior $p(	heta|x)$. It's a clever way to tackle the challenges of Bayesian inference while still providing a principled and computationally efficient approach.

---
# Another arriving at ELBO:

Given the three key points we have discussed:

1. In Bayesian inference, we want to compute the posterior distribution $p(	heta|x)$, but the evidence $p(x)$ is often intractable.

2. Variational inference introduces a variational distribution $q(	heta)$ to approximate the true posterior $p(	heta|x)$.

3. The goal is to find the optimal variational distribution $q^*(	heta)$ that minimizes the KL divergence between $q(	heta)$ and $p(	heta|x)$:

   $q^*(	heta) = rg\min_{q(	heta)} KL(q(	heta) || p(	heta|x))$

   where the KL divergence is defined as:

   $KL(q(	heta) || p(	heta|x)) = \int q(	heta) \log rac{q(	heta)}{p(	heta|x)} d	heta$

We now want to find a way to optimize the variational distribution $q(	heta)$ without having to compute the intractable evidence $p(x)$. In other words, we need an objective function that we can maximize or minimize to find the best approximation to the true posterior, while avoiding the computation of $p(x)$.

This is where the ELBO comes into play. By deriving the ELBO from the KL divergence, we can obtain a lower bound on the log evidence $\log p(x)$ that depends only on the joint distribution $p(x, 	heta)$ and the variational distribution $q(	heta)$. Maximizing this lower bound will be equivalent to minimizing the KL divergence between $q(	heta)$ and $p(	heta|x)$, which is our ultimate goal.

So, our motivation and what we want to achieve can be summarized as follows:

- We want to find an objective function that allows us to optimize the variational distribution $q(	heta)$ to approximate the true posterior $p(	heta|x)$ without having to compute the intractable evidence $p(x)$.

- We aim to derive a lower bound on the log evidence $\log p(x)$ that depends only on the joint distribution $p(x, 	heta)$ and the variational distribution $q(	heta)$, which we can maximize to find the best approximation to the true posterior.

With this motivation in mind, we can now proceed to derive the ELBO from first principles by starting from the KL divergence and manipulating the terms to obtain the desired lower bound.

(... The derivation of the ELBO follows as in the previous response ...)

By clearly stating our motivation and what we want to achieve, we provide a solid foundation for deriving the ELBO from first principles. This helps to understand why the ELBO is a crucial component of variational inference and how it enables us to optimize the variational distribution without computing the intractable evidence.

# What does it mean when we make the assumption that "we have Gaussian priors over the parameters"?
When we assume Gaussian priors over the parameters in a Bayesian neural network, it means that we believe the parameters (weights and biases) of the network follow a Gaussian (normal) distribution before observing any data.

Suppose we have a neural network with $L$ layers, and each layer $l$ has $K_l$ neurons. The weights and biases of layer $l$ are denoted as $\mathbf{W}_l$ and $\mathbf{b}_l$, respectively.

Assuming Gaussian priors over the parameters means:
1. For each weight $w_{ij}^{(l)}$ connecting neuron $i$ in layer $l-1$ to neuron $j$ in layer $l$:
   $w_{ij}^{(l)} \sim \mathcal{N}(\mu_{w,ij}^{(l)}, {\sigma_{w,ij}^{(l)}}^2)$
   where $\mathcal{N}(\mu, \sigma^2)$ denotes a Gaussian distribution with mean $\mu$ and variance $\sigma^2$.
2. For each bias $b_j^{(l)}$ of neuron $j$ in layer $l$:
   $b_j^{(l)} \sim \mathcal{N}(\mu_{b,j}^{(l)}, {\sigma_{b,j}^{(l)}}^2)$

The prior distribution over all the weights and biases in the network is then given by:

$p(\mathbf{W}, \mathbf{b}) = \prod_{l=1}^L \prod_{i=1}^{K_{l-1}} \prod_{j=1}^{K_l} \mathcal{N}(w_{ij}^{(l)} | \mu_{w,ij}^{(l)}, {\sigma_{w,ij}^{(l)}}^2) 