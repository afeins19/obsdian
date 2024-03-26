simple linear models 
- all attributes are numeric
- represents linear boundaries between classes 

SVMs are extensions of simple linear models
- nonlinear class boundaries
- transforming the input using a nonlinear mapping
- a straight line in the new space doesn't look straight in the original space 
### Key ideas
- new effecient separability of non linear regions use **kernel functions**
- use quadratic optimization problem to avoid local minimum issues that occur with neural nets 
- an optimization algorithm rather than a greedy algorithm 
# Approximating the decision boundary 
![[Screen Shot 2024-02-28 at 1.36.30 PM.png]]
- using polynomial regression may be used to find the more complex boundary lines but this is intensive and may result in overfitting 

# Hyperplane
the set described by a single scalar product equality 
- this set of points orthogonal to w (our vector)

we try to find a hyperplane H such that $\{H= x|w^tx=b\}$
which is orthogonal to w, shifted by b. 

![[Screen Shot 2024-02-28 at 1.52.21 PM.png]]
# Maximum Margin Hyperplane 

![[Screen Shot 2024-02-28 at 1.37.39 PM.png]]
a hyperplane has dimension (n-1) in a space of dimension n. SVM algorithms try to find a hyperplane that best separates the classes based on statistical approaches. It finds the maximum margin between the hyperplane which means it finds the maximum distances among classes. 

We want a hyperplane which provides the maximum margin, the max sized hyperplane between 2 classes. Support vectors are data points that lie closest ot the decision surface (or hyperplane). **These data points are the most difficult to classify since they are on the boundary of 2 categories. They have a direct bearing on the location of the hyperplane** 

![[Screen Shot 2024-02-28 at 1.52.37 PM.png]]

# Support Vectors 
![[Screen Shot 2024-02-28 at 1.58.22 PM.png]]

![[Screen Shot 2024-02-28 at 1.59.38 PM.png]]

### Properties of SVM Hyperplanes 
- there will be at least one support vector for each class
- SVMs optimize by finding hyperplanes with maximum margins between them

### How an SVM classifier works 
- SVMs is optimized by finding hyperplanes with maximum margins between them 
- the decision function is really specified by a small subset of training points 
- done by a trivial quadratic algorithm

![[Screen Shot 2024-03-11 at 1.38.24 PM.png]]

### Margin Maximization 
we want a classifier (linear separator) with as big a margin as possible 
![[Screen Shot 2024-03-11 at 1.45.45 PM.png]]
note that the distance from a point ($x_0, y_0$) is to a line $Ax+By+c=0$ is 
$$\frac{|Ax_0 + By_0 + c|}{\sqrt{A^2+B^2}}$$

### Defining the Constraint of maximal margins 
- integrating condition on $H_1$  and $H_2$  
![[Screen Shot 2024-03-11 at 1.47.00 PM.png]]

this is a quadratic programming problem for maximizing the margin:
- Min f(w) with g(w) = 0 or $Min(\frac{||w||^2}{2})$ 
- we can solve this constraint problem using the lagrangian multiplier method 
- the solution is a quadratic which describes the surface of a parabaloid (3d parabola) with just a **single global minimum**  
![[Screen Shot 2024-03-11 at 1.50.58 PM.png]]

when x_i is not a support vector, a_i will be 0, since we have to solve the equation for a large set of points, the optimization equation automatically filters all points that are not linear combinations of the support vectors.

![[Screen Shot 2024-03-11 at 1.59.04 PM.png]]

# Non-Linear SVMs 
sometimes, training data is not linearly separable 
![[Screen Shot 2024-03-11 at 2.02.09 PM.png]]

this is not a trivial task but we can get an idea for it by seeing the transformation into a higher dimensional mapping 

![[Screen Shot 2024-03-11 at 2.04.02 PM.png]]
by mapping from $R^1$ to $R^2$, we can now separate these 2 classes. 
### Kernel Trick 
![[Screen Shot 2024-03-11 at 2.08.58 PM.png]]
these allow us to measure the similarity between 2 elements in the transformed space. 

below are some of the functions we used to define point affinity in the transformed space. Note these functions are agnostic to the actual transformation but are applicable. 
![[Screen Shot 2024-03-11 at 2.12.35 PM.png]]

### Kernel Functions 
how do we test accuracy? say that a script takes a single image file and predicts if there is a bird in the image or not. Say we use 15000 images for validation and our model has a correct answer 95% of the time. How accurate is this model? even if it answered incorrectly for images with birds, this test data would conclude that our model is 95% accurate. We need a new way to classify accuracy: 

- true positives 
- true negatives 
- false positive
- false negative 

### Defining Performance Measures
- precision : true positive/ all positive guesses 
- recall: true positive/total birds
- accuracy: (true positive + true negative) / (total number of tests)
- F1 score: $2*\frac{precision * recall}{prcesision + recall}$ - the harmonic mean of these measures 

say precision is 0.5 and recall is 0.1. Average is 0.3 but our F1 score would be 2((0.5*0.1)/0.6) = 0.1888 

### SVM Implementation
- support vector classification (SVR for regression)
- the multi-class support is handled according to a one-vs-one scheme 

```
sklearn.svm.SVC(*,C=1.0,kernel='rbf',degree=3,gamma='scale',coef0=0.0)
```
- c: regularization parameter
- kernel:{linear, poly, rbf, sigmoid, precomputed} 
- degree: int, defaut = 3, degree of the polynomial kernel function 
- gamma: scale or auto



