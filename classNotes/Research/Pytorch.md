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
In case you have a GPU, you should now see the attribute `device='cuda:0'` being printed next to your tensor. The zero next to cuda indicates that this is the zero-th GPU device on your computer.











