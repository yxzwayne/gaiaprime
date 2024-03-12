Two questions need to be answered in order to fully specify the updates:
(a) Which coordinate to choose?
(b) How to set the new value of $w_i$?

Give answers to these questions, and thereby flesh out a coordinate descent method. For (a), your solution should do something more adaptive than merely picking a coordinate at random.
Then implement and test your algorithm on a logistic regression problem.

We use the wine dataset.
# Experiment Instructions
- Begin by running a standard logistic regression solver (e.g., from scikit-learn) on the training set. It should not be regularized: if the solver forces you to do this, just set the regularization constant suitably to make it irrelevant. Make note of the final loss L∗.
- Then, implement your coordinate descent method and run it on this data.
- Finally, compare to a method that chooses coordinates i uniformly at random and then updates wi using your method (we’ll call this “random-feature coordinate descent”).
- Produce a clearly-labeled graph that shows how the loss of your algorithm’s current iterate— that is, L(wt)—decreases with t; it should asymptote to L∗. On the same graph, show the corresponding curve for random-feature coordinate descent.
# Report content

1. Description of coordinate descent method
	1. give a description of how I solve (a) and (b). 
	2. Do I need L(•) to be differentiable, or have continuous second-order derivatives?
	3. or does it work with any cost function?
2. Convergence
	1. Under what conditiosn will my method converge to the optimal loss?
	2. No need to prove, but give a few sentence of explanation.
3. Experimental results
4. Evaluation
	1. Do you think there is scope for further improvement in your coordinate descent scheme in (1); if so, how?
5. Sparse coordinate descent
	1. Now, suppose we want a k-sparse solution w: that is, one that has at most k nonzero entries.
		1. Propose a modified version of your method for this task. Assume k is part of the input, along with the data.
		2. Do you think this method always find the best k-sparse solution when L(·) is convex?
		3. Try this out on the wine data. Make a table of loss values obtained for a few selected values of k.
# Working Drafts
### 1. Which coordinate should we choose?
Given the problem of updating one parameter at a time, we are presented with some intuitive approahces:
- **Cyclic Coordinate Descent:** This method involves iterating through the coordinates in a fixed order. After updating the last coordinate, the process starts over with the first coordinate. While simple, its performance can be highly dependent on the ordering of the coordinates. Also, we can straight up reason that this will not be the best performant because this method cannot adapt to the training dynamics, which is wasting critical information that would otherwise have been leveraged.
- **Random Coordinate Descent:** Instead of following a fixed sequence, we can select a coordinate to update at random. Because this process encodes more entropy, the training dynamics can be potentially better than cyclic coordinate descent, but formal proof is required to verify this.
- **Greedy (or Gauss-Southwell) Rule:** Here, the coordinate with the highest gradient (in absolute value) is chosen for the update. This method assumes differentiability of \(L(w)\) and can lead to faster convergence since it prioritizes coordinates that promise the greatest immediate decrease in the loss function.

### 2. How do we set the new values of $w_i$?

The update mechanism for the chosen coordinate \(i\) depends on the form of the loss function \(L(w)\) and can involve different strategies:

- **Exact Line Search:** If the cost function \(L(w)\) is differentiable and convex along the direction of the \(i\)-th coordinate, one could use exact line search to find the optimal update. This involves minimizing \(L(w)\) with respect to \(w_i\) while keeping the other coordinates fixed, which may require solving a one-dimensional optimization problem.

- **Gradient-Based Update:** If \(L(w)\) is differentiable, a gradient-based update could be applied. For example, \(w_i\) could be updated by moving in the direction opposite to the partial derivative of \(L(w)\) with respect to \(w_i\), scaled by a step size. The step size could be constant, diminishing, or determined by a line search method.

- **Proximal Update:** In cases where \(L(w)\) includes non-differentiable components (e.g., regularization terms), proximal methods can be applied. This involves solving a simpler optimization problem that approximates the original problem but is easier to solve for the \(i\)-th coordinate.

### Existing Approaches and Enhancements

Coordinate descent algorithms have been extended and improved in various ways, including:

- **Block Coordinate Descent:** Instead of updating a single coordinate at a time, this variant updates a block of coordinates. This can be useful when certain groups of coordinates are related or when the optimization problem naturally decomposes into subproblems with multiple variables.

- **Accelerated Coordinate Descent:** Techniques like Nesterov’s acceleration can be adapted for coordinate descent to improve convergence rates, especially for smooth convex functions.

- **Parallel and Distributed Coordinate Descent:** In settings where computation can be parallelized, multiple coordinates can be updated simultaneously, either in a shared-memory or distributed computing environment. This requires careful handling of dependencies and data consistency to ensure convergence.

Coordinate descent methods offer simplicity and efficiency, particularly for large-scale optimization problems where evaluating the gradient or Hessian of the entire vector \(w\) is computationally expensive. Their effectiveness, however, can vary significantly depending on the structure of the cost function \(L(w)\) and the specifics of the implementation, such as the coordinate selection rule and the update mechanism.


# Reading notes

## Paper: https://arxiv.org/pdf/1506.00552.pdf
- show that, compared to the usual constant step-size update of the coordinate, the GS method with exact coordinate optimization has a provably faster rate for problems satisfying a certain sparsity constraint (Section 5)
- in Section 6, we propose a variant of the GS rule that, similar to Nesterov’s more clever randomized sampling scheme, uses knowledge of the Lipschitz constants of the coordinate-wise gradients to obtain a faster rate

To flesh out a coordinate descent method for a logistic regression problem, we'll implement a variant that uses a more adaptive approach than random coordinate selection. We'll adopt the Greedy selection rule (Gauss-Southwell rule), where we choose the coordinate with the largest gradient magnitude. This approach tends to select the coordinate that is most misaligned with the current gradient, suggesting it could lead to a significant decrease in the loss if updated.

### Coordinate Descent for Logistic Regression

Logistic regression models the probability that a target variable belongs to a particular class. For binary classification, the model is defined as:

\[ P(y = 1 | x; w) = rac{1}{1 + e^{-w^Tx}} \]

where \(x\) is the feature vector, \(w\) is the weight vector, and \(y\) is the binary target variable. The cost function \(L(w)\) for logistic regression, typically the negative log-likelihood with \(L2\) regularization, is given by:

\[ L(w) = -\sum_{i=1}^n [y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i)] + rac{\lambda}{2} \|w\|^2 \]

where \(\hat{y}_i\) is the predicted probability for the \(i\)-th instance, and \(\lambda\) is the regularization parameter


# Report Drafts

## 1. Description of Coordinate Descent Method
### 1.1 Approach to Solving the Optimization Problem
The coordinate descent method optimizes an objective function by iteratively updating one coordinate (or parameter) at a time while keeping all other coordinates fixed. This process involves two key decisions at each iteration: which coordinate to update (a) and how to set the new value for this coordinate (b).
#### (a) Choice of Coordinate:
In our custom logistic regression implementation, we adopt an adaptive approach to choosing the coordinate by selecting the one with the largest absolute value of the gradient. This strategy is based on the intuition that the coordinate with the largest gradient magnitude contributes most to the loss and, therefore, offers the most potential for reduction in the objective function upon updating.

#### (b) Setting New Values for \(w_i\):
The new value for the chosen coordinate \(w_i\) is determined by applying a simple gradient descent update rule, specifically adjusting \(w_i\) in the direction opposite to its partial derivative. This approach requires specifying a learning rate, which controls the size of the step taken in the direction of the steepest decrease.

### 1.2 Differentiability Requirements

For the coordinate descent method to be applicable, the objective function \(L(