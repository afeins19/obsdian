Deep learning is essentially just a Large Neural Network.. It may also be defined as **Hierarchical Feature Learning**. This means that the algorithm automatically has the ability to discover and learn good representations of the data using feature learning. 
- makes learning algorithms much better and easier to use
- performance just keeps getting better as we feed in more data 
### Why Deep Learning? 
- deep implies large number of layers
- the model will converge onto better performance simply by increasing the training data 
![[Pasted image 20240415140153.png]]

the benefit of deep learning is that, given enough data, we don't really need to worry about feature engineering. The network will itself extract the most relevant features during training. 

In theory, deep learning neural networks (CNNs) form a representation of features from low-level to high-level as we move through more and more layers.  

# Challenges 
- III-conditioning
- gradient exploding

# Optimization Methods 
data aggregation 
- stochiastic method
- minibatch
- regular batch

updating algorithms
- stochastic gradient descent

Parameter Initialization 
- Orthogonal Initialization 
- Random Initialization
- Normalized Initialization 
- Sparse Initialization 

Adaptive Learning Rate 
- AdaGrad
- RMSProp
- **Adam** 

# Weight Initialization 
the first step that comes into consideration when building a neural network 

Determines the: 
- convergence time 
- convergence point 

### Zero Initialization
a common init type (not great) set everything to zero 

### Random initialization
better than zero init but may cause some slow learning based on how far our initial points are on the loss function 


### He Initialization
- activation aware initialization of weights (for ReLu)
- ReLu and leaky ReLu solves the vanishing gradient problem 
$$RandomInit \times \sqrt{\frac{2}{inputsize}}$$
constrains the range of weights from each input layer to some reasonable range. 


