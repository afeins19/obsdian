# Standard ML Libraries 
```python 
import math
import numpy as np 
import time 

# Plotting libraries 
import matplotlib.pyplot as plt 
%matplotlib inline

from IPython.display import set_matplotlib_formats 
set_matplotlib_formats('svg','pdf') # For export

from maplotlib.colors import to_rgba

import seaborn as sns 
sns.set() 

# Progress bar 
from tqdm.notebook import tqdm
```

# Importing PyTorch
```python 
import torch 

# for funsies
print("Using Torch Version: ", torch.__version__)
```

# Torch Seed 
seed to allow users to reproduce the same random values consistently. 
```python 
torch.manual_seed(42)
```

# Tensors 
a tensor is a mathematical object that generalizes the concept of scalars, vectors, and matrices to higher dimensions.

## Creating a Tensors with Pytorch 

### Populating Tensors
*note: just running`torch.tensor` will reuse any value that has already been in memory.*
```python 
# reusing values that are already in memory
x_default = torch.Tensor(2, 3, 4)

# populating with zeros
x_zeros = torch.zeros(2,3,4)

# random values between 0 and 1 
x_rand = torch.rand(2,3,4)

# random values samples from a normal distribution 
x_randn = torch.randn(2,3,4)
```

### Ordered Values
creates a tensor containing the values $N,N+1,N+2\\,...,M$

```python 
x_arranged = torch.arrange(2,3,4)
```

## Getting Tensor Attributes 
you can get the shape of tensors just like in numpy with `x.shape` or `x.size`.
```python 
shape = x.shape
size = x.size()

dim1, dim2, dim3 = x.size()
print("Size:", dim1,dim2,dim3) 
```

## Converting Between Tensor & Numpy
you can convert between numpy arrays and tensors (and vice-versa). 

Note: **The conversion of tensors to numpy requires  the tensor to be on the CPU**, and not the GPU (more on GPU support in a later section). In case you have a tensor on GPU, you need to call `.cpu()` on the tensor beforehand. Hence, you get a line like **`np_arr = tensor.cpu().numpy()`**.

### Numpy to Pytorch 
```python 
np_arr = np.array([[1,2], [3,4]])
tensor = torch.from_numpy(np_arr) 

print("Numpy Array:", np_arr)
print("PyTorch Tensor:", tensor) 
```

```
Numpy array: [[1 2] [3 4]]
PyTorch tensor: tensor([[1, 2], [3, 4]])
```

### Pytorch to Numpy 
```python 
tensor = torch.arange(4) # single dim tensor of range(0,4)
np_arr = tensor.numpy()

print("PyTorch Tensor:", tensor)
print("Numpy Array:", np_arr)
```

```
PyTorch tensor: tensor([0, 1, 2, 3])
Numpy array: [0 1 2 3]
```

## Operations 

### Addition 
the sum of two tensors is a new tensor containing the sum of the two input tensors. 
```python
x1 = torch.rand(2,3)
x2 = torch.rand(2,3)

y = x1 + x2
```

```
X1 tensor([[0.1053, 0.2695, 0.3588],
        [0.1994, 0.5472, 0.0062]])
X2 tensor([[0.9516, 0.0753, 0.8860],
        [0.5832, 0.3376, 0.8090]])
Y tensor([[1.0569, 0.3448, 1.2448],
        [0.7826, 0.8848, 0.8151]])
```

### Reshaping (View)
tensors may be reshaped to any size so long as it can hold the same number of elements. For example, a tensor of size (2,3) can be reshaped to size (6), (3,2), etc. This operation is called **View**.

```python 
x = torch.arrange(6)
print("X", x) # X tensor([0, 1, 2, 3, 4, 5])

x = x.view(2,3)
print("X", x) # X tensor([[0, 1, 2], [3, 4, 5]])

```

### Matrix Multiplication 
Neural Networks often require us to take an input  vector $X$ and transform it using a learned weight matrix $W$. Below are the common ways to perform this operation. 

```python 
# setting up a tensor 
x = torch.arange(6)
W = torch.arange(9).view(3,3) # operation stacking is allowed 

# performing multiplication 
h = torch.matmul(x, W) 
```

The behavior depends on the dimensionality of the tensors as follows:

- If both tensors are 1-dimensional, the dot product (scalar) is returned.
    
- If both arguments are 2-dimensional, the matrix-matrix product is returned.
    
- If the first argument is 1-dimensional and the second ￼￼￼
argument is 2-dimensional, a 1 is prepended to its dimension for the purpose of the matrix multiply. After the matrix multiply, the prepended dimension is removed.
    
- If the first argument is 2-dimensional and the second argument is 1-dimensional, the matrix-vector product is returned.
    
- If both arguments are at least 1-dimensional and at least one argument is N-dimensional (where N > 2), then a batched matrix multiply is returned. If the first argument is 1-dimensional, a 1 is prepended to its dimension for the purpose of the batched matrix multiply and removed after. If the second argument is 1-dimensional, a 1 is appended to its dimension for the purpose of the batched matrix multiple and removed after. The non-matrix (i.e. batch) dimensions are [broadcasted](https://pytorch.org/docs/stable/notes/broadcasting.html#broadcasting-semantics) (and thus must be broadcastable). For example, if `input` is a (j×1×n×n)(j×1×n×n) tensor and `other` is a (k×n×n)(k×n×n) tensor, `out` will be a (j×k×n×n)(j×k×n×n) tensor.
    
    Note that the broadcasting logic only looks at the batch dimensions when determining if the inputs are broadcastable, and not the matrix dimensions. For example, if `input` is a (j×1×n×m)(j×1×n×m) tensor and `other` is a (k×m×p)(k×m×p) tensor, these inputs are valid for broadcasting even though the final two dimensions (i.e. the matrix dimensions) are different. `out` will be a (j×k×n×p)(j×k×n×p) tensor.
### In-Place Operations
instead of creating a new tensor, we can use the `<operation>_` prefix to perform the operation in place. *Note: for most operations, appending a '_' will imply that it is to be done **in-place***

```python 
x1 = torch.rand(2, 3)
x2 = torch.rand(2, 3)

print("X1 (before)", x1)
print("X2 (before)", x2)

x2.add_(x1) # adds x1 to x2

print("X1 (after)", x1)
print("X2 (after)", x2)
```

```
X1 (before) tensor([[0.7539, 0.1952, 0.0050],
        [0.3068, 0.1165, 0.9103]])
X2 (before) tensor([[0.6440, 0.7071, 0.6581],
        [0.4913, 0.8913, 0.1447]])
X1 (after) tensor([[0.7539, 0.1952, 0.0050],
        [0.3068, 0.1165, 0.9103]])
X2 (after) tensor([[1.3979, 0.9024, 0.6632],
        [0.7981, 1.0078, 1.0550]])
```
## Stacking Operations 
operations may be stacked as well
```python 
W = torch.arange(9).view(3,3)
```

```
W tensor([[0, 1, 2],
        [3, 4, 5],
        [6, 7, 8]])
```

## Indexing Tensors
Indexing for tensors is the same as in numpy 
```python
x = torch.arrange(12).view(3, 4) # tensor of size (x,y,z) = (3,4,3)

"""
		X tensor([[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11]])
"""

# printing the second column 
print(x[:1]) # tensor([1, 5, 9])

# printing the first row 
print(x[0]) # tensor([0, 1, 2, 3])

# printing the first 2 rows of the last column 
print(x[:2, -1]) # tensor([3,7])
```

# Dynamic Computation Graph & Backpropagation
Pytorch automatically support gradient/derivative calculations for the functions that we define. If we use weight matrices in our function that we want to learn, then those are called the *parameters* or just *weights*. 

If our neural network would output a single scalar value, we would talk about taking the **derivative**, but more often than not, we will have multiple output variables so we would refer to the output as a **gradient**. 
### The Computational Graph
Given some input $x$, we define our function by *manipulating* that input, usually by matrix multiplication with weight matrices and addition operations with bias *bias vectors*.  

As we perform operations over our input, Pytorch automatically creates a *computational graph* of these operations. This shows us the ordered sequence of steps needed to arrive at a given output. PyTorch is a *define-by-run* framework which means that it automatically generates and maintains the graph as we perform manipulations on our data

### Gradients 
> **Note: Why do we want gradients?** Consider that we have defined a function, a neural net, that is supposed to compute a certain output y for an input vector x. We then define an **error measure** that tells us how wrong our network is; how bad it is in predicting output y from input x. Based on this error measure, we can use the gradients to **update** the weights W that were responsible for the output, so that the next time we present input x to our network, the output will be closer to what we want.

we must first specify **which tensors require gradients to be computed**. By default, a newly created tensor will not require a gradient unless specified. 

```python 
x = torch.ones((3,))
print(x.requires_grad) # False 
```

This can be changed for an exiting tensor by using the `requires_grad_()` function (underscore indicating an in-place operation) or passed as an argument to an initializer when creating a new tensor. 

```python 
# For existing tensor
x.requires_grad_(True)
print(x.requires_grad) # True 

# Or in the  nitializer 
y = torch.ones((3,), requires_grad=True)
```

### Gradient Computation Example 
Say we define our gradient function as such (where $\ell(x)$ denotes the number of elements). 

$$y = \frac{1}{\ell(x)}\sum_i \left[(x_i + 2)^2 + 3\right]$$
we are taking a mean here over the operation within the sum. You could imagine that x are our parameters, and we want to optimize (either maximize or minimize) the output y. For this, we want to obtain the gradients ∂y/∂x. For our example, we'll use x=<0,1,2> as our input.

We can express this operation in our code as well and see how PyTorch handles the computation graph to enable back propagation. 

```python 
x = torch.arange(3, dtype=torch.float32, requires_grad=True) # Only float tensors can have gradients

print("X", x)

a = x + 2
b = a ** 2
c = b + 3
y = c.mean() 
print("Y", y)
```

```
Y tensor(12.6667, grad_fn=<MeanBackward0>)
```


These operations can be represented by this graph: 

![[Pasted image 20240827130450.png]]

PyTorch automatically calculates the gradient of each step of the calculation so we can express the gradient of our composite function $y$ using the chain rule: 

$$\frac{\partial y}{\partial x_i} = \frac{\partial y}{\partial c_i}\frac{\partial c_i}{\partial b_i}\frac{\partial b_i}{\partial a_i}\frac{\partial a_i}{\partial x_i}$$

Each of the partial derivatives are are taken with respect to their argument terms:

$$
\frac{\partial a_i}{\partial x_i} = 1,\hspace{1cm}
\frac{\partial b_i}{\partial a_i} = 2\cdot a_i\hspace{1cm}
\frac{\partial c_i}{\partial b_i} = 1\hspace{1cm}
\frac{\partial y}{\partial c_i} = \frac{1}{3}
$$
So in summary, with an input vector of $x = [0,1,2]$, the gradients are $\partial y/\partial \mathbf{x}=[4/3,2,8/3]$.



# GPU Support 

PyTorch supports the functionality for performing computations on both CPUs and GPUs. We can define a `device()` object to conditionally select to run on either processor depending on whether or not the machine running the code has a gpu or not

```python 
device = torch.device("cuda") if torch.cuda.is_available() else torch.device("cpu")

print("Device", device)
```
we can then push a tensor to the selected device 

```python 
x = torch.zeros(2, 3)
x = x.to(device)

print("X", x)
```

In case you have a GPU, you should now see the attribute `device='cuda:0'` being printed next to your tensor. The zero next to cuda indicates that this is the zero-th GPU device on your computer.

**NOTE!!!:** When generating random numbers, the seed between CPU and GPU is not synchronized. Hence, we need to set the seed on the GPU separately to ensure a reproducible code. Note that due to different GPU architectures, running the same code on different GPUs does not guarantee the same random numbers.

### Setting the Seed for CPU & GPU
```python 
# GPU operations have a separate seed we also want to set
if torch.cuda.is_available():
torch.cuda.manual_seed(42)
torch.cuda.manual_seed_all(42)

# Additionally, some stochastic operations are implemented on the GPU for efficiency

# We want to ensure that all operations are deterministic on GPU (if used) for reproducibility

torch.backends.cudnn.deterministic = True
torch.backends.cudnn.benchmark = False
```

# Training Neural Networks with Torch 
its possible train neural networks by directly specifying the weight and bias matricies with Tensors (with `requires_grad=True`) and have PyTorch compute the gradients and make adjustments. But this is hella complicated, especially for projects with many parameters. 

# Example: Continuous XOR 


**Problem Statement**: Given two binary inputs $x_1$ & $x_2$, we want the neural network to predict 1 if and only if ONE of the inputs is 1 and to predict 0 for all other cases.

### Packages
the `torch.nn` package streamlines the process of building neural networks. This is what we'll be using. 
```python 
# importing
import torch.nn as nn 
import torch.nn.functional as F 
```
additionally, the `torch.nn.functional` package contains functions that are used in network layers. This is in contrast to `torch.nn` which defines functions as objects encapsulated in *modules* that are chained together. (I THINK) `torch.nn.functional` just contains the raw function code and then it may be used within specific modules. 

### Modules 
in PyTorch, we create neural networks out of modules. **Modules** can contain other modules and a neural network is considered to be a module itself too. below is a basic module template
```python 
class SuperCoolModule(nn.Module):

	def __init__(self):
		super().__init__()
		# write subclass init code for this module 

	def forward(self, x):
		# Function that performs this modules calculation
		pass 

```

 In the init function, we usually create the parameters of the module, using `nn.Parameter`, or defining other modules that are used in the forward function

### Creating a Simple Classifier 
Below, we will create a simple classifier of the following model 
![[Pasted image 20240829143638.png]]
**input neurons**: blue 
**hidden neurons**: white
**output neurons**: red

note that to represent the XOR gate we are using 2 input neurons, 4 hidden neurons, and 1 output neuron for the result. 

```python 
class SimpleClassifier(nn.Module):

	def __init__(self, num_inputs, num_hidden, num_outputs)
		super().__init__()

		# initializing the modules to build the layers of our nn
		self.linear_input = nn.Linear(num_inputs, num_hidden)
		self.act_fn = nn.Tanh()
		self.linear_output = nn.Linear(num_hidden, num_outputs)

	def forward(self, x):
		# processing the input through the network 
		x = self.linear_input(x)
		x = self.act_fn(x)
		x = self.linear_output(x)
		return x 
```
This is the basic structure of the model, but we need to train it for it to function correctly. 

*Note that we do not apply a sigmoid on the output yet. This is because other functions, especially the loss, are more efficient and precise to calculate on the original outputs instead of the sigmoid output.*

### Getting Model Attributes 
```python 
model = SimpleClassifier(num_inputs=2, num_hidden=4, num_outputs=1)

# printing a modell shows all of tis submodules 
print(model)

for name, param in model.named_parameters():
	print(f"Parameter {name}, shape {param.shape}")
```

```
SimpleClassifier( (linear1): Linear(in_features=2, out_features=4, bias=True) (act_fn): Tanh() (linear2): Linear(in_features=4, out_features=1, bias=True) )


Parameter linear1.weight, shape torch.Size([4, 2]) 
Parameter linear1.bias, shape torch.Size([4]) 
Parameter linear2.weight, shape torch.Size([1, 4]) 
Parameter linear2.bias, shape torch.Size([1])
```

Each linear layer has a weight matrix of shape `[output, input]`, and a bias of shape `[output]`. The tanh activation function has no parameters. 

**Parameters are only registered for `nn.Module` objects that are direct object attributes**!!! 

## Generating and Preparing Data  
PyTorch has some built-in functionality to streamline the process of loading testing and training data. 
```python
import torch.utils.data as data 
```
PyTorch defines **two classes** for handling data. This is the standard interface for working with your data
- **`data.Dataset`** - provides a uniform interface to access the training and test data 
- **`data.DataLoader`** - efficiently loads and stacks data points from the dataset in training batches 

### The Dataset Class 
To define a dataset in PyTorch, we just need to write two functions:
- `__get_item__` - returns the $i$-th data point in the dataset
- `__len__` - returns the size of the dataset 

### The XOR dataset 
below is the code that will create our dataset for the continuous XOR model

```python
class XORDataset(data.Dataset):

	def __init__(self, size, std=0.1):
		"""
			class inputs: 
				size - number of data points to make 
				std - the standard deviation of added noise    
		"""
		super().__init__()
		self.size = size
		self.std = std
		self.generate_continous_xor() # function to make data 

	def generate_continous_xor(self): 
		# Each data point in the XOR dataset has 2 variables (x and y)
		# the label is the output of x XOR y 

		data = torch.randint(low=0, high=2, size=(self.size, 2),
		dtype=torch.float32)
		label = (data.sum(dim) == 1).to(torch.long) # XOR 

		# introducing gaussian noise 
		data += self.std * torch.randn(data.shape)

		self.data = data
		self.label = label 

	def __len__(self):
		return self.size 

	def __getitem__(self, idx): 
		data_point = self.data[idx]
		data_label = self.label[idx]
		
		return data_point, data_label # returns a tuple
```

now we can create the dataset and inspect it 
```python 
import torch
dataset = XORDataset(size=200)

print("Size of dataset:", len(dataset))
print("Data point 0:", dataset[0])
```
example of generated output from these print calls (will differ as data is randomly generated but the size doesn't change)
```
Size of dataset: 200 Data point 0: (tensor([0.1060, 0.9192]), tensor(1))
```
### Visualizing the Data
below is some code to plot and visualize the data 
```python 
def visualize_samples(data, labbel):
	if isinstance(data, torch.Tensor):
		data = data.cpu().numpy() # note that we must use cpu for numpy
	if isinstance(label, torch.Tensor): 
		label = label.cpu().numpy()

	data_0 = data[label == 0] # all datapoints with label=0
	data_1 = data[label == 1] # all datapoints with label=1

	plt.title("Dataset samples")
	plt.figure(figsize=(4,4))
	plt.scatter(data_0[:,0], data_0[:,1], edgecolor="#333", label="Class 0")

	plt.scatter(data_1[:,0], data_1[:,1], edgecolor="#333", label="Class 1")
	
	plt.ylabel(r"$x_2$")
	plt.xlabel(r"$x_1$")
	plt.legend()
```
```python 
visualize_samples(dataset.data, dataset.label)
plt.show()
```

![[Screen Shot 2024-08-29 at 3.22.32 PM.png]]

### The Data Loader Class 
This class `torch.utils.data.DataLoader` represents an iterable dataset with support for:
- automatic batching 
- multi-process data loading 
- etc. 

**the data loader communicates with the dataset using the `__getitem__` function and stacks the outputs as tensors over the first dimension to form a batch**. Unlike the dataset class, we usually don't have to define our own data loader. Instead we can create an object and mold it with the following input parameters
- `batch_size: int` - Number of sample to stack per batch
- `shuffle: bool` - If True, data is returned in a random order 
- `num_workers: int` - the number of sub processes used for data loading. The default is 0 which means that data will be loaded in the main process which can be slow for things like images where data points are huge
- `pin_memory: bool` - If True, the data loader will copy Tensors into CUDA pinned memory before returning them. This can save time for large datapoints on GPUs. 
- `drop_last` - If True, the last batch is dropped in case it is smaller than the specified batch size. This occurs when the dataset size is not a multiple of the batch size. This is helpful when you want to keep a consistent batch size 

	below is a simple data loader. 
	- `next(iter(data_loader))` gets the first batch of the data loader. 
	- If `Shuffle=True`, a different batch gets returned each time this code is run 
	- since the DataLoader() object is iterable, we can use a for-each loop 

```python 
data_loader = data.DataLoader(dataset, batch_size=8, shuffle=True)

data_inputs, data_labels = next(iter(data_loader))

print("Data inputs", data_inputs.shape, "\n", data_inputs)
print("\n")
print("Data labels", data_labels.shape, "\n", data_labels)
```

Example output (note values are random but sizes are always consistent)

```
Data inputs torch.Size([8, 2]) 
tensor([[ 1.0843, 1.0192], [ 1.0060, -0.0828], [ 0.9584, 0.1025], [ 1.0558, 0.8975], [ 0.0921, 1.0137], [-0.0387, -0.0767], [-0.0124, 1.0740], [ 1.0348, 0.9924]])

Data labels torch.Size([8]) 
tensor([0, 1, 1, 0, 1, 0, 1, 0])
```

## Optimization 
After defining the model and the dataset. Optimization involves the following steps: 
1. Get a batch from the data loader 
2. Run the batch through the model and get its predictions 
3. Calculate the loss based on the difference b/w predictions and labels
4. Backpropogation - find the gradient for every parameter w.r.t the loss
5. Update the parameters based on the calculated gradients 

## Loss Modules 

we can find the loss for a batch by doing a few tensor operations (Which are automatically added to the computation graph). For binary classification we can use the **Binary Cross Entropy (BCE)** function:
$$\mathcal{L}_{BCE} = -\sum_i \left[ y_i \log x_i + (1 - y_i) \log (1 - x_i) \right]$$
- y = labels
- x = predictions 
- both x,y are in range $[0,1]$

PyTorch already provides us with modules that are loss functions. The BCE Function above has two analogs in PyTorch
- `nn.BCELoss()` - expects the inputs of x to be in range $[0,1]$
- `nn.BCEWithLogitsLoss()` - contains sigmoid layer and a bce loss layer. This makes the model more numerically stable (idk why)

```python 
loss_module = nn.BCEWithLogitsLoss()
```

# Stochastic Gradient Descent 
PyTorch provides the `torch.optim` package that implements many of the most popular optimization algorithms. For this form gradient descent (SGD), we will use `torch.optim.SGD`. Recall that his updates parameters by multiplying the gradients with a small constant (the learning rate) and subtracts them from the parameters (minimizing the loss function), 

The input to the optimizer are the parameters of the model: `model.parameters()`
```python
# learning rate = 0.1
optimizer = torch.optim.SGD(model.parameters(), lr=0.1) 
```

### Optimizer Parameters 
The optimizer provides two functions for adjusting parameters:
- `optimizer.step()` - updates the parameters based on the gradients 
- `optimizer.zero_grad` - sets the gradients of all parameters to **zero**, this is done before performing back propagation. If we don't make the gradients zero after training, then the last gradient values will be added back to the previous ones 

# Training 
Now we are ready to begin training. First we must create a slightly larger data set and create a data loader with a larger batch size. Note that for small datasets, pushing to the GPU takes much more time than just running it all on the CPU but if the dataset is large, then its best to use the GPU.

```python 
# creating large XOR data set with large batch size 
train_dataset = XORDataset(size=2500)
train_data_loader = data.DataLoader(train_dataset, batch_size=128, shuffle=True)
```

Now we can push the data to our selected device: 
```python 
model.to(device)
```

### Training Function 
Before training (but within the training function), we must set our model to training mode by calling `model.train()`. This is done because certain modules need to perform a different forward step during training than during testing (BatchNorm and Dropout). To switch to the testing mode, call `model.eval()`

```python
def train_model(model, optimizer, data_loader, loss_module, num_epochs=100):
	# Training loop
	for epoch in tqdm(range(num_epochs)):

		# Step 1: Move input data to device (if using gpu)
		data_inputs = data_inputs.to(device)
		data_labels = data_labels.to(device)

		# Step 2: Run the model on input data 
		preds = model(data_inputs)
		# since output is [batch size,1] we want just [batch size]
		preds = preds.squeeze(dim=1)

		# Step 3: Calculate loss 
		loss = loss_module(preds, data_labels.float())

		# Step 4: Backpropagate 
		# ensure that gradients are all zero before starting
		optimizer.zero_grad()

		# Backpropgate
		loss.backward()

		# Step 5: Update Parameters 
		optimizer.step() 
```

now we can call the function and train the model on our dataset 
```python 
train_model(model, optimizer, train_data_loader, loss_module)
```

# Saving a Trained Model 
Models can be saved, specifically the weights tensor can be saved to a `state_dict`. To save a model, just do:
```python
state_dict = model.state_dict()
torch.save(state_dict, "my_model.tar")
```

### Loading a Model from a `state_dict`
```python
state_dict = torch.load("my_model.tar")

# creating a new model and loading in the state
new_model = SimpleClassifier(num_inputs=2, num_hidden=4, num_outputs=1)
new_model.load_state_dict(state_dict)
```
if we print the `state_dict` of the original model and the new_model, we can see that they are the same.

# Evaluation 
we remove some portion of data from the dataset for testing purposes. For the XOR example, our dataset consists of pre-generated data so we have to make some more data points for testing. 

```python 
test_dataset = XORDataset(size=500)

# drop_last...don't do it in this case 
test_data_loader = data.DataLoader(test_dataset, batch_size=128, shuffle=False, drop_last=False)
```

### Accuracy Metric
$$acc = \frac{\#\text{correct predictions}}{\#\text{all predictions}} = \frac{TP+TN}{TP+TN+FP+FN}$$

  
where TP are the true positives, TN true negatives, FP false positives, and FN the false negatives.

### Deactivating The Computational Graph
When we evaluate the model, we don't need to keep track of the computation graph since we wont be calculating the gradients. This lets us free up compute and memory that was required for that to speed up the model. 

To deactivate the computational graph, we can use `with torch.no_grad():`
```python 
def eval_model(model, data_loader):
	model.eval() # sets the model to eval mode
	true_preds, num_preds = 0., 0. # setting up values for formula

	with torch.no_grad():
		for data_inputs, data_labels in data_loader:

			# Get the model's predictions for the 
			data_inputs = data_inputs.to(device)
			data_labels = data_labels.to(device)

			# Store model predictions
			preds = model(data_inputs)
			preds = preds.squeeze(dim=1)
			preds = torch.sigmoid(preds) # Sig forces data b/w 0 & 1
			pred_labels = (preds >= 0.5).long() # binarize preds

			# Compute true predictions (TP+TN)
			true_preds += (pred_labels == data_labels).sum()
			num_preds += data_labels.shape[0]

	acc = true_preds / num_preds
	print(f"Model Accuracy: {100.0*acc:4.2f}%")
```

```python
eval_model(model, test_data_loader)
```

# Visualizing Classification Boundaries

to visualize what the model has learned, we can perform a prediction for every data point in a range of $[-0.5, 1.5]$. This will tell us where the model has created decision boundaries and which points would be classified as 0 or 1. This visualization will show us the following:
- if a point would fall in class 0, we'd see a blue background
- if a point would fall in class 1, we'd see an orange background 
- if the model is uncertain about a particular region, we'll see a blurry overlap 

```python 
@torch.no_grad() # Decorator, same effect as "with torch.no_grad(): ..." over the whole function.

def visualize_classification(model, data, label):

	if isinstance(data, torch.Tensor):
		data = data.cpu().numpy()
	if isinstance(label, torch.Tensor):
		label = label.cpu().numpy()
		data_0 = data[label == 0]
		data_1 = data[label == 1]
		
	  
	
	fig = plt.figure(figsize=(4,4), dpi=500)
	
	plt.scatter(data_0[:,0], data_0[:,1], edgecolor="#333", label="Class 0")
	plt.scatter(data_1[:,0], data_1[:,1], edgecolor="#333", label="Class 1")
	
	plt.title("Dataset samples")	
	plt.ylabel(r"$x_2$")	
	plt.xlabel(r"$x_1$")
	plt.legend()
	
	  
	
	# Let's make use of a lot of operations we have learned above
	
	model.to(device)
	
	c0 = torch.Tensor(to_rgba("C0")).to(device)
	c1 = torch.Tensor(to_rgba("C1")).to(device)
	
	x1 = torch.arange(-0.5, 1.5, step=0.01, device=device)
	x2 = torch.arange(-0.5, 1.5, step=0.01, device=device)
	
	xx1, xx2 = torch.meshgrid(x1, x2, indexing='ij') # Meshgrid function as in numpy
	
	model_inputs = torch.stack([xx1, xx2], dim=-1)
	preds = model(model_inputs)
	preds = torch.sigmoid(preds)
	
	output_image = (1 - preds) * c0[None,None] + preds * c1[None,None] # Specifying "None" in a dimension creates a new one
	
	output_image = output_image.cpu().numpy() # Convert to numpy array. This only works for tensors on CPU, hence first push to CPU
	
	plt.imshow(output_image, origin='lower', extent=(-0.5, 1.5, -0.5, 1.5))
	
	plt.grid(False)
	
	return fig

  

_ = visualize_classification(model, dataset.data, dataset.label)

plt.show()
```
   ![[Pasted image 20240830182328.png]]

# TensorBoard
This tool lets us visualize how our training_loss decreases over time 
```python 
writer = SummaryWriter(logging_dir)

model_plotted = False
# Add average loss to TensorBoard

epoch_loss /= len(data_loader)

writer.add_scalar('training_loss',

epoch_loss,

global_step = epoch + 1)

  

# Visualize prediction and add figure to TensorBoard

# Since matplotlib figures can be slow in rendering, we only do it every 10th epoch

if (epoch + 1) % 10 == 0:

	fig = visualize_classification(model, val_dataset.data, val_dataset.label)
	
	writer.add_figure('predictions',
	
	fig,
	
	global_step = epoch + 1)

  

writer.close()

```
