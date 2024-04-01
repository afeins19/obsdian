improvement on the gradient descent algorithm. Featuring the following additions to the model: 
- regularization
- tree pruning 
- parallelization 
- GPU acceleration 

### Regularization (avoids overfitting) 
- we penalize the overfitting model in XGB 
	- l1 reg to minimize the magnitude of feature wheight 
	- l2 reg to minimize the power of feature weight 

### Parallelization
- sequential nautre in GBM is exploited 

### Missing Data Handling 
- has its own in-built missing data handler whereas gbm doesnt 
- sparsity-aware split finding 
	- learns the imputation strategy as it constructs the trees during the training process 



