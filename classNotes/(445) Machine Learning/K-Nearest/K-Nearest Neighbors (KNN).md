Parametric vs Nonparametric models
# Parametric Models
estimates **parameters** from the training dataset to learn a function that can classify new data points without requiring the original training dataset anymore 
- the number of parameters is fixed 

some parametric models are: 
- the perceptron 
- logistic regression 
- linear svm 

# Nonparametric data
the number of parameters **grows with the training data**
- instance-based learning (memorizing the training dataset)
- Trained model uses the training data explicitly 
# KNN 
a supervised learniner for both classification and regression tasks
- with classification, we can predict categorical class membership
- for regression, we can predict a target members value 
### Pros & Cons
**pros**
- immediately adapts with new training data

**cons**
- computational complexity for classifying new samples grows linearly with the number of samples in the training data set in the worst case scenario (we can use trees to reduce this complexity)
- storage space can become a challenge with large datasets 
### Steps for KNN 
1. choose the number of N and a distance measure 
2. Find the N-nearest neighbors of the sample that we what to classify
3. assign the class label by the majority group near the observed element 

### Distance Metric Selection
it's important to choose a good measure for distance measurement. The right choice provides for a good balance between over and under fitting. 

a common choice is the **Minkowski Distance** a generalization of euclidean distance. 
$$d(x^{(i)},x^{(j)})= \sqrt[p]{\sum_k|{x^{(i)}_k-x^{(j)}_k}|^p}$$
# Overfitting Problem
KNNs are particularly sensitive to overfitting. Even the closest neighbors may be too far away in a high-dimensional space to give a good estimate. 

![[Screen Shot 2024-02-09 at 1.47.33 PM.png]]
- note how much the size along each dimension increases as the total dimensions increases 

# GridSearchCV  
optimizer for any machine learning model. Takes in models and parameters. The sklearn.model_selection.GridSearchCV from scikitlearn automatically searches over specified parameter values fro an estimator 

**estimator**: object
- assumed to implement the scikit-learn estimator interface
- either estimator needs to provide a score function or some scoring function must be passed in 

**param_grid**: dict or list of dicts
- names as keys and lists of parameter settings to try as values or a list of such dictionaries 

