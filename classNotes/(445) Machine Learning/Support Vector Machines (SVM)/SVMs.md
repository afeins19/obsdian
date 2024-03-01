simple linear models 
- all attributes are numeric
- represents linear boundaries between classes (to simple for practice applications)

SVMs are extensions of simple linear models
- nonlinear class bboundaries
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