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

# Torch Seed 
seed to allow users to reproduce the same random values consistently. 
```python 
torch.manual_seed(42)
```

# Tensors 
a tensor is a mathematical object that generalizes the concept of scalars, vectors, and matrices to higher dimensions.

## Creating a Tensors with Pytorch 

### Populated with Random Values
```python 
# default random values
x_default = torch.Tensor(2, 3, 4)
print(x)

# random values between 0 and 1 
x_rand = torch.rand(2,3,4)

# random values samples from a normal distribution 
x_randn = torch.randn(2,3,4)
```

### Ordered Values
creates a tensor containing the values $N,N+1,N+2\\,...,M$

```python 
x_arrange = torch.arrange(2,3,4)
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

Note: **The conversion of tensors to numpy require the tensor to be on the CPU**, and not the GPU (more on GPU support in a later section). In case you have a tensor on GPU, you need to call `.cpu()` on the tensor beforehand. Hence, you get a line like **`np_arr = tensor.cpu().numpy()`**.

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

# Reshaping (View)
tensors may be reshaped to any size so long as it can hold the same number of elements. For example, a tensor of size (2,3) can be reshaped to size (6), (3,2), etc. This operation is called **View**

```python 
x = torch.arrange(6)
print("X", x) # X tensor([0, 1, 2, 3, 4, 5])

x = x.view(2,3)
print("X", x) # X tensor([[0, 1, 2], [3, 4, 5]])

```

### In-Place Operations
instead of creating a new tensor, we can use the `<operation>_` prefix to perform the operation in place 

```python 
x1 = torch.rand(2, 3)
x2 = torch.rand(2, 3)

print("X1 (before)", x1)
print("X2 (before)", x2)

x2.add_(x1)

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



