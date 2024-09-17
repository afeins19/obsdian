bellow is a step-by-step explanation of computing the final result which are the amounts to change the weights of some neuron with activation value $a_j^{(l)}$ which is in some layer $l$:

# We want to compute in the end: **$$\frac{\partial L}{\partial W_{ij}^{(l)}}$$**
### First, Apply the Chain Rule to Compute $\frac{\partial L}{\partial a_j^{(l)}}$
where $L$ is the loss function and $a_j^{(l)}$ is the activation function of a particular neuron in layer $l$ (the current layer),  

### Second, compute the change in the activation of the current function WRT to the preactivation: $\frac{\partial a_j^{(l)}}{\partial z_j^{(l)}}$ 
This tells you how much the activation function changes with respect to its input $z_j^{(l)}$ - this term is the sum of all inputs from the previous layer into the current layer, given by: 
$$z_j^{(l)} = \sum_i W_{ij}^{(l)} a_i^{(l-1)}+ b_j^{(l)}$$
- $W_{ij}^{(l)}$ - weight of a particular connection of neuron i in (l-1) and j in (l)
- $a_i^{(l-1)}$ - activation value from neuron i in layer (l-1) 
- $b_j^{(l)}$ - bias value of the current layer l 

### Third, Compute how the pre-activation sum $z_j^{(l)}$ changes WRT its input weights: $\frac{\partial z_j^{(l)}}{\partial W_{ij}^{(l)}}$
This tells us the effect each weight has on the pre-activation sum. For each $\forall W_{ij} \in$ Layer L, the partial derivative only depends ton the current weight.    

Since for a given connection from layer $l-1$ to layer $l$, the pre-activation term for that connection can be expressed as:
$$
z_j^{(l)} = \sum_i W_{ij}^{(l)} a_i^{(l-1)}+ b_j^{(l)}
$$
We get the following partial derivative: 
$$\frac{\partial z_j^{(l)}}{\partial W_{ij}^{(l)}} = a_i^{(l-1)}$$

# Putting It All Together 
$$\frac{\partial L}{\partial W_{ij}^{(l)}} = \frac{\partial L}{\partial a_j^{(l)}} \cdot \frac{\partial a_j^{(l)}}{\partial z_j^{(l)}} \cdot \frac{\partial z_j^{(l)}}{\partial W_{ij}^{(l)}} = \frac{\partial L}{\partial a_j^{(l)}} \cdot\sigma'(z_j^{(l)}) \cdot a_i^{(l-1)}
$$
This corresponds to the change in the loss function with respect to each weight in a given layer. This is then propagated backwards to be used recursively in the calculations for the previous layer. The gradient for a neuron $j$ in layer $l$ can be expressed as a column vector: 
$$\nabla_{W_j^{(l)}} L = \begin{bmatrix} 
\frac{\partial L}{\partial W_{1j}^{(l)}} \\
\frac{\partial L}{\partial W_{2j}^{(l)}} \\
\vdots \\
\frac{\partial L}{\partial W_{nj}^{(l)}}
\end{bmatrix}
$$




