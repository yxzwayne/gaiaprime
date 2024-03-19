Given:
- m: the number of input features to the layer.
- n: the number of output features (neurons) of the layer.
- key: a seed for random number generation to ensure reproducibility.
- scale: a scaling factor for the parameter values, defaulting to 1e-2.

Algorithm:
1. Split the input \texttt{key} into two separate keys, \texttt{w\_key} and \texttt{b\_key}, for generating weights and biases respectively.
   \[ \texttt{w\_key}, \texttt{b\_key} = \texttt{random.split}(\texttt{key}) \]

2. Generate the weights matrix of shape \((n, m)\) by drawing samples from a normal distribution, scaled by the \texttt{scale} parameter. This matrix is initialized using \texttt{w\_key}.
   \[ W = \texttt{scale} \times \texttt{random.normal}(\texttt{w\_key}, (n, m)) \]

3. Generate the biases vector of length \(n\) by drawing samples from a normal distribution, scaled by the \texttt{scale} parameter. This vector is initialized using \texttt{b\_key}.
   \[ b = \texttt{scale} \times \texttt{random.normal}(\texttt{b\_key}, (n,)) \]

4. Return the weights matrix \(W\) and biases vector \(b\) as the layer parameters.
   \[ \text{return} \ (W, b) \]
   