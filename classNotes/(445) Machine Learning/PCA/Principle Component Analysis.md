# Principle Component Analysis (PCA)
an unsupervised learning technique used for **reducing the dimensionality of the data**. The method of representing the data with **approximately equivalent data in a reduced dimension**. PCA is considered to be part of data preprocessing.

We do PCA because **some features are redundant and/or noisy**! 
- ex: data with 100 different variables from sensors 
- only 2 sensors might have significant information 
- 10 sensors have sometimes marginal data
- 88 sensors have insignificant information 
- pick just a few of the first components that satisfy the problem 

PCA involves transforming observed variables into a set of latent variables such that we lose minimal data when dropping into a lower dimension. 
![[Screen Shot 2024-02-26 at 1.32.48 PM.png]]

### Principle Components 
the **direction of the data that explain a maximal amount of variance**
- the lines that capture the most amount data 

![[Screen Shot 2024-02-26 at 1.35.46 PM.png]]
### Applications of PCA
- visualizing multidimensional data
- compressing information
- simplification of complex business decisions 

### Advantages 
- easy to compute 
- speeds up other machine learning algorithms 
- counteracting the issues of high-dimensional data by preventing overfitting 

### Disadvantages 
- low interpretability of principle components
	- not easy to interpret the "meaning" of each component. This is because each data point can be plotted by some linear combination of the other attributes 
- trade off between information loss and dimensionality reduction 
- it doesn't directly consider the correlation between the principal components and the target variable in the original dataset 

PCA also suffers from some llimitations
- sensitive to the scale of features (so we must standardize the data)
- not robust against outliers (biased against strong outliers)

# Procedure 
a dataset with N samples has D features. X is the data set represented as a matrix 
$$X=\begin{bmatrix} 
X_1^{T} \\
X_2^{T} \\
X_3^{T} \\
\vdots 
\\X_n^T
\end{bmatrix} \in \mathbb{R^{n\times D}}$$

we want to find a new orthonormal basis in D that **best approximates X**
![[Screen Shot 2024-02-26 at 2.04.24 PM.png]]
![[Screen Shot 2024-02-26 at 2.04.49 PM.png]]

1. standardize the range of continuous initial variables
2. compute the covariance matrix of standardized variables 
3. compute the eigenvectors and eigenvalues of the covariance matrix to identify the principal components
4. decide which principal components to keep and create a transformation matrix
5. recast the data along the new principal component axes 

### 1. Standardizing 
standardize the data to the range of continuous initial variables to "fairly" represent their contributions 
$$Z = \frac{value - mean}{std. dev}$$

### 2. Compute Covariance Matrix ![[Screen Shot 2024-02-26 at 2.08.01 PM.png]]

# 3. Find Eigenvectors 
![[Screen Shot 2024-02-26 at 2.08.25 PM.png]]

![[Screen Shot 2024-02-26 at 2.08.52 PM.png]]

### 4. Decide what to keep 

![[Screen Shot 2024-02-26 at 2.09.11 PM.png]]
- typically we try to aim for principle components which cover **90%** of the data 