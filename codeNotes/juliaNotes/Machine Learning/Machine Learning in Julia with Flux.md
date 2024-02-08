**Link**: https://www.youtube.com/watch?v=9nhVaJSuMF8&ab_channel=WestDRI

# Artificial Neurons ![[Screen Shot 2024-01-17 at 4.59.08 PM.png]]
- a neuron is connected to neurons in the previous layer
- the weighted sum from all the other neurons is summed and then passed through some activation function before being passed to our neuron 

# Artificial Neural Network 
![[Screen Shot 2024-01-17 at 5.01.23 PM.png]]
	this is a single artificial neural network (ANN). All ANNs feature an input layer, some hidden layer(s) and an output layer. If our neural network is used for images, we pass in a vector representing the pixel values for each pixel. 

- **Fully Connected** - each neuron in the nth layer is connected to every neuron from the (n-1)th layer 

- **Feed-Forward** - there are no loops in the network. All data flows in a single direction

- **Deep Neural Network** - a neural network with more than one hidden layer (which would be called a shallow neural network)

# Activation Function  
	biological neurons have a binary response to stimuli, either on or off. The input only triggers activation if it exceeds some threshold. The activation function in ANNs models this behavior.

These activation functions generally collapse the input into a binary output (on or off). 
### Common Activation Functions 
- ReLu, or Sigmoid activation functions are quite popular activation functions 
### Bias 
	a constant term we may sum with some vector to ~bias~ our activation function in some direction (either up or down) - an offset. 

# Supervised Learning 
we are given a set of example input/output pairs:
$$(x_i, y_i)$$
**Goal -** if X is the space of inputs and Y is the space of outputs, find a function h such that 
$$\forall x_i \in X,\, h_\theta(x_i) \,\text{is a predictor for the corresponding value} \: y_i$$
we then use these pairs to find the relationship between inputs and outputs. For the continuous case, we use **regression** and for the discrete case, we use **classification**. 

# Unsupervised Learning 
we don't have any labeled data, we are only given a set of training data 
$$x_i$$
**Goal** - Look for some structure within the data 
**look into cocktail party algorithm**

### Loss Function 
unsupervised machine learning is all about minimizing the loss function that we use to measure our models accuracy. A classic approach is to use Gradient Descent. 

### Overfitting 
this is a common challenge of machine learning. This is when noise in the data is being interpreted as meaningful when in reality it is not. This occurs when the model matches itself too closely to our training data and captures features that are in fact just noise. 

![[Screen Shot 2024-01-17 at 5.33.49 PM.png]]
	the green line overfits the model but the black line is ideal. If we have too many predictors (Variables) we tend to over-fit, too few, we under-fit. 
### Solutions to Overfitting
- regularization by adding a penalty to the loss function 
- stopping early (before we have time to overfit)
- increase depth (more layers)
- decrease breadth (less neurons per layer) - this reduces the overall number of parameters but creates vanishing and exploding gradient problems 
a good approach is also to adapt our neural network to our particular problem and data - fewer and shared parameters (cnn, rnn explained later)

# Convolutional Neural Network (CNN)
	used for spatially structured data (e.g. image recognition) 
consider color images on a 28 x 28 grid of pixels. Each pixel has 3 values to represent the rgb values of that pixel, so our input layer consists of this many neurons! 
$$ 28 \times 28 \times 3 = 2352$$
the subsequent layer of n neurons (if fully connected) would receive this many connections!
$$n(2352)$$
### Convolutional Layers
we solve this problem using **convolutional layers**. This is where neurons receive input from a subarea (called a local receptive field) of the previous layer. This cuts down the number of parameters. 

### Pooling (optional approach)
pooling combines the outputs of neurons in a subarea to reduce the data dimensions. The *stride* dictates how the subarea is moved across the image. Max-pooling uses the **maximum** for each subarea

# Recurrent Neural Network (RNN)
	used for chain-structured data (e.g. Text). Specifically data that has been structured in some chain. 

![[Screen Shot 2024-01-17 at 5.59.12 PM.png]]

----------------------------------------------------
# Implementation 

### Popular ML Libraries (python or general)
- PyTorch - facebook AI research lab
- TensorFlow - Google Brain Team 

*note: julia is well suited for the implementation of mathematical models. GPU Kernels can be written directly in Julia. Julia is also an incredibly fast language.* 

### Popular Julia ML packages 
- Flux.jl - a machine learning stack
- Knet.jl - deep learning framework
- TensorFlow.jl - wrapper for TensorFlow
- Turing.jl - probabilistic machine learning 
- MLJ.jl - framework to compose machine learning models 
- SciKitLearn.jll - implementation of the scikit-learn API

we will be looking at Flux.jl 

--> Goto Julia Note Book on ML 


