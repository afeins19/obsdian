# Early Boolean Circuit Model of the brain
takes a summation of linear terms and applies a non-linear function to produces some output
![[Screen Shot 2024-04-08 at 1.46.58 PM.png]]
# Hebbian Learning 
when a group of neurons fire together, they wire together. This is modeled in the following way: 

![[Screen Shot 2024-04-08 at 1.52.09 PM.png]]

the change in weight for some cells is some constant factor of the number of connected neurons that fire to it. 

# Perceptron 
adjusts the connection among neurons to match the output to the target value we want 
- a very simple linear classifier 

# Forward Propagation
after taking the weighted sums, we can apply some non-linear activation functions. We may also apply some type of bias to the sum.
![[Screen Shot 2024-04-08 at 2.01.00 PM.png]]

# Activation Functions 
![[Screen Shot 2024-04-08 at 2.02.51 PM.png]]
these functions are used to define how the weighted sum of the input is transformed into an output from a node
- decision for a final output
- linear activation function
- non-linear activation models 

# Nonlinear Activation Functions 
- sigmoid: output layer for binary classification 
- hyperbolic tangent: faster than sigmoid due to higher derivative 
- ReLU
	- many zeros
		- good for fast implementation
		- bad for losing information 
- leaky ReLU 
	- instead of mapping all negative values to 0, it instead maps them to some smaller negative number 

# Training the Perceptron
- feed in multiple training samples and calculate the output for each of hem 
- adjust the weights w for each sample to minimize the output error (loss)
	- output error: the difference between the desired and actual outputs
		- $e = y_{target} - y_{predict}$ 
- loss may be defined differently for each specific task 

### Single Perceptron Drawbacks 
it can only learn linearly separable functions. In fact, it is literally impossible to implement the XOR function 
![[Screen Shot 2024-04-10 at 1.44.53 PM.png]]
there is no way to draw a line through these points that distinguishes the 2 classes (0 or 1) without at-least 1 error 

to overcome this we can: 
- multilayer perceptron 
- composing a bunch of perceptrons together 

# Muti Output Perceptron 
![[Screen Shot 2024-04-10 at 1.45.43 PM.png]]
$$w_1 = w_{11} + w_{12} + w_{13}$$
# Feedforward NN
after the input passess through the 4 hidden layer perceptrons, we can then pass the output through another series of neurons (in the next layer)
![[Screen Shot 2024-04-10 at 1.49.14 PM.png]]

# Quantifying Loss 
![[Screen Shot 2024-04-10 at 1.53.53 PM.png]]
in order to optimize the weights, we need to derive a metric of performance for our model  - the loss function. The cost function is a function of our predictions $X^{(i)}$ and a weight $W$ as well as the actual value for that training sample $y^{(i)}$ 
# Beyond Linearity 
if each perceptron in a multilayer neural network is only allowed to use a linear activation function, the final output of our network will still be some function of the inputs
- the feedforward neural network is no more powerful than the perceptron no matter how many layers it has 
# Back propagation 
the most essential part of learning. This tunes the weights by seeing what values we must tune the weights to minimize the loss function 
![[Screen Shot 2024-04-10 at 2.12.12 PM.png]]
# Gradient 
a vector which operates on a scalar function to produce a vector whose magnitude is the maximum rate of change of the function at the point of the gradient 

# Training the Perceptron 
1. training sample is presented and propagated forward through the network 
2. the output error is calculated, typically the mean squared error ($\frac{(t-y)^2}{2}$)
3. Network error is minimized using gradient descent 
	- a stochastic approximation of the gradient descent optimization method for minimizing an objective function 
	- the wheight's are update in such a way that we don't overstep the global minimum (wheight's are just a small scalar)
# Stochiastic Gradient Descent 
$$\Delta_{w_{ij}} = -\alpha \frac{dQ}{dw_{ij}}$$ where Q is our error function and $w_{ij}$ is the weight of input i to neuron j 

# Batched Stochiastic Gradient Descent 
if we take the gradient for each training data point, we may converge very slowly but we might also, have a chance of being knocked off from a local minimum and find a global minimum (a global minimum convergence value). This process how ever is quite slow and involves a rather inefficient path through the loss function. We can take the gradient based on the average of a sequence of values (say groups of 10) - this is called **mini-batching**. This lets us take fewer steps towards a minimum value but might result in having us enter a local minimum rather than the global. The benefit of taking the gradient at each data point is that we have a higher chance of being put on a path towards a lower minimum value.
# Universal Approximation Theorem 
for a single layer network with a finite number of neurons, this network can be trained to approximate an arbitrarily random function
- a single hidden layer is powerful enough to learn any function 

this is a theoretical proof and in reality we want to have multiple layers to learn the function quicker. 
# Components of Neural Networks
- input layer x
- arbitrary amount of hidden layers 
- output layer y_hat 
- set of weights and biases between each layer, W and b 
- a choice of activation function for each hidden layer - $\sigma$ 

```python
class NeuralNetwork:
	def __init__(self, x,y):
		self.input = x 
		self.weight1 = np.random(self.input.shape[1],4) # 4 neurons in input layer 
		self.weight2 = np.random.randint(4,1)
		self.y = y
		self.output = np.zeros(y.shape)
```

# Back-propagation 
![[Pasted image 20240415132806.png]]

![[Pasted image 20240415133006.png]]

we take the derivatives over the activation functions. The input to these activation functions is a linear function of $w$. The gradient w.r. to the loss function consists of the 3 terms above d(loss(y,y_hat)/dy, dy_hat/dz, and dz/dw. These relate only to the the **last layer** in the sequence of activations 

### Back Propogation Implementation 
```python 
class NN:
	def __init__(self, x, y):
		self.input = x
		...
def feedforward(self):
	# calculates activation value for each neuron to the next in the layer 
		self.layer1 = sigmoid(np.dot(self.input, self.weights1))
	...

def backprop(self):
	# applying the chain rule
	d_weights2 = np.dot(self.layer1.T (2*(self.y_act-y_pred)))...
```

