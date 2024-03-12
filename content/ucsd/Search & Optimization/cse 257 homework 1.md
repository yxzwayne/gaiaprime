Yuxuan (Wayne) Zhang
A15120059
# Question 1 Plotting Level Sets

## 1.1
$f_1(x_1,x_2)=x_1x_2$

![[1-1 levelset.png]]

## 1.2
$f_2(x_1,x_2,x_3)\ =$  3-variable Gaussian Density with 1/2/1 as diagonals of the covariance matrix.

![[1-2 levelset.png]]

## 1.3
$f_3(x_1,x_2,x_3) = \int_{-\inf}^{\inf}{f_2(x_1,x_2,x_3)dx_3}$

Reasoning:
Integrating $x_3$ out of the function is known as marginalizing it out. since the 3d level set is shaped like the above (a dome), we can conveniently imagine that marginalizing $x_3$ is like collapsing, or projecting the 3d shape, onto the linear space formed by $x_1$ and $x_2$. Then, thinking about how Gaussian distribution is parametrized by mean and variance, we can use the same mean between $x_1$ and $x_2$ and a reduced variance of 1 and 2, to imagine that our level set will be an ellipse with a 2 to 1 a to be ratio (i forgot how to exactly define this.)

![[1-3 levelset.png]]

# Question 2
## 2.1
1. **Initialization**:
  - Set a sufficiently small step size $lpha$, such that it can maintain the validity of first-order approximations within the neighborhood of each point.

2. **Iteration** (for $k = 0, 1, 2, \ldots$):
  - Generate a random unit vector $d_k$ in the input space.
  - Compute two new points along this direction spaced by the step size $lpha$:
    - $x_{k+1}^+ = x_k + lpha d_k$
    - $x_{k+1}^- = x_k - lpha d_k$
  - Evaluate the function $f$ at $x_k$, $x_{k+1}^+$, and $x_{k+1}^-$ by comparing $f(x_k)$, $f(x_{k+1}^+)$, and $f(x_{k+1}^-)$.
  - Choose the point with the lowest function value as the next iteration's starting point $x_{k+1}$.

3. **Termination Criterion**: Continue until a specified number of iterations is reached or the decrease in function value falls below a threshold, indicating convergence or a local minimum.

## 2.2 Custom Three-Point Method
![[2-2.png]]

## 2.3 Gradient Desent
![[2-3 gradient descent.png]]

## 2.4
Explain why, for any continuous function with n-dimensional input space, estimating its gradient takes n samples at any input. Then, given the difference in the sample size of each iteration between three-point methods and gradient descent using estimated gradient for blackbox functions, combined with the performance you plotted, explain the pros and cons of each method.
### Answer
The gradient of a function at any point is a vector of its partial derivatives with respect to each input dimension. this means that every input dimension needs to be considered at least once in the procss of gradient estimation, if we are to adequately "estimate" the gradient without knowing what it actually is.

From the plot comparison, gradient descent reliably decrease (optimize) to minimum quicker than 3-point methods. This means that using gradient descent can often save compute resources if we implement early stopping. If we know the gradient information, functions in higher order dimensions leverage gradient descent better than pure random exploration.

However, we don't always have access to the gradient information of a function. This makes the three point method a reasonable substitute as a last resort. Three point can also be sample/resource efficient when obtaining the gradient needs more resource than computing three evaluations.

# Question 3

## 3.1 Describe First Two Steps of Optimal Step Size
![[3-1.jpeg]]
![[3-1-step2.jpeg]]

## 3.2
![[3-2.jpeg]]

# Question 4
## 4.1 
![[4-1.png]]
## 4.2
![[4-2.png]]

## 4.3 Newton Descent
![[4-3.png]]
this converged kinda quickly.
# Question 5
Prove that gradient descent with exact line search should always take orthogonal directions in each iteration.

![[5.jpeg]]

# Question 6
1. $f_1(x) = x_1^2 + x_2^2$
2. $f_2(x) = -rac{ 1 + cos(12\sqrt{x_1^2 + x_2^2}) }{0.5(x_1^2 + x_2^2) + 2}$
3. $f_3(x) = \sum_{i=1}^{50} x_i^2$
## 6.1
Plotting function 2
![[6-1.png]]
## 6.2 Simulated Annealing
![[6-2 SA 1.png]]
## 6.3 Cross Entropy Method
![[6-3 cem 1.png]]
## 6.4 Search Gradient

My implementation did not run into the "Covariance is not positive-semidefinite" Error. However, this may arise when attempting to sample from a Gaussian distribution with a covariance matrix that is not positive-semidefinite. 
- A quick ask to ChatGPT told me it could be due to numerical instability or rounding errors during updates.
- In my code, I probed the function values produced with covariance-involved algorithms, and many of them yield nan after a few iterations. Because we can still plot the output, just with limited iterations, I just tried to not update the covariance matrix when that happens. 
- Turns out, the outcome plot makes a lot of sense.
- I'm guessing that Jax can auto-handle errors on non-psd covariance matrices computation and just propagate to function values? That would also make sense.

![[6-4 search gradient 1.png]]

## 6.5

Some speculations I have regarding method comparison can be regarding the sampling freedom. 
- How will the degree of sampling affect the convergence of each algorithm?
To answer this question, I will need to fix a function and a k, and run 3 algorithms using the same sampling coefficient and plot the results on the same plot. 

![[6-5 comparison 1.png]]

From the plot, we can see that simulated annealing and search gradients take much irregular optimization paths compared to cross entropy methods. When annealing works, it will go near the optimal space reached by cross-entropy methods, due to its exploratory nature. However, simulated annealing suffers from the curse of dimensionality, which means in higher dimensional space, it may be better to use cross entropy methods or search gradient. This is demonstrated in the function 3 performance, where simulated annealing failed to catch the performance of CEM. However, I am surprised that SA did not converge on function 2. I'd think exploration will make it work huh. 

Since the CEM curve is much smoother and tends to decrease faster, it is generally the most high-performing algorithm over a lot of function settings (convexity, dimension). SA shows more variability, which can be good for escaping local minima but might also lead to less stable convergence. SG appears to be sensitive to the choice of step size and the normalization of the gradient, which can affect its performance.
For smooth, convex problems, I would recommend use gradient-based methods like search gradient.
If the problem is noisy and non-convex, I would consider using cross entropy methods for its reliability.
