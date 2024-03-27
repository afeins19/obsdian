The goal of ensembels is combine different classifiers into a meta-classifier that has better general performance than each individual classifier alone. We train these models using m different classifiers 
$$(C_1,...,C_m)$$
# Majority Voting 
![[Screen Shot 2024-03-20 at 1.34.15 PM.png]]

### sklearn library
```python 
sklearn.ensemble.VotingClassifier
```

-  Soft Voting/Majority Rule classifier for unfitted estimators  
- Estimators: list of (str, estimator) tuples  
-  Voting: {‘hard’, ‘soft’}, default=’hard’  
-  Weights: array-like of shape (n_classifiers,), default=None (uniform weights)  


# Random Forest Algorithm
an ensemble method which combines different decision tree classifiers with majority voting 

# Describing Ensemble Models
we select a class label $y' = mode\{C_1(x),...,C_m(x)\}$      
- the assumption that all n-base classifiers for a binary classification task have an equal error rate 
- assumes that the classifiers are independent and the fact that the error rates are not correlated 
- the error probability of an ensemble of base classifiers as a PMF of a binomial distribution: 
$$ P(Y>=k) = \sum_k^n{n\choose k}\epsilon^k(1-\epsilon)^{n-k}$$

### Implementing a simple majority vote classifier
majority vote (Weighted):
$$y' = arg \max_i \sum_{j=1}^m{w_jX_A(C_j(x)=i)}$$
the weights can be set by evaluating the performance of each classifier and weighting its performance accordingly. So classifiers with better  will weigh heavier on the vote instead of using a majority system. 
![[Screen Shot 2024-03-20 at 1.47.37 PM.png]]

# Bagging 
The building of an ensemble of classifiers from bootstrap samples. We use bootstrap samples (Random samples with replacement) from the initial training set. 

Bagging allows us to reduce the variance of the dataset. 


### Random Forest
a technique used to improve the accuracy of unstable models and decrease the degree of **overfitting** 
- applicable to both classification and regression problems effectively 

**Procedure**:
1. a subset of data points and a subset of features is selected for constructing each base model. n records and m features are taken from the data set having k number of records k>=n
2. construction of individual models from each base sample
3. each base model generates an output
4. final output is considered based on majority voting or averaging for classification 

