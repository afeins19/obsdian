an algorithm based on Bayes Theorem, it's used for learning and classification. It uses **prior** probability of each category given no further other information about an item. Categorization produces a **posterior** probability distribution over the possible categories given a description of some item. 
- easy to impllement 
- good results obtained in most cases
- we must assume class independence -> loss of accuracy 
- more dependencies exist among variables in practical examples 

**Goal:** we want to select the class with the highest probability.  

![[Screen Shot 2024-02-19 at 1.29.56 PM.png]]
to work with this data, we need to calculate the prior probability of each piece of data (play=yes/no) given each attribute 

![[Screen Shot 2024-02-19 at 1.35.18 PM.png]]

We now have a series of lookup tablels with probabilities for each situation. Using naive bayes, we can multiply over a specific series of events to get a prediction for an event. 

![[Screen Shot 2024-02-19 at 1.39.14 PM.png]]
we can determine that x' is no by applying bayes. 

# Handeling Continuous Attributes 

![[Screen Shot 2024-02-19 at 1.50.12 PM.png]]
- the issue here is that we have some continuous data and no discrete values for prior probabilities or the likely hood of each event
- to resolve this we construct a continuous distribution (specifically Gaussian distribution)
### Likelihood for some event over a continuous distribution 

$$% Gaussian Naive Bayes formula for a single feature
P(x | c) = \frac{1}{\sqrt{2\pi\sigma_{c}^2}} \exp\left(-\frac{(x - \mu_{c})^2}{2\sigma_{c}^2}\right)

% Where:
% - P(x | c) is the probability of feature x given class c.
% - \mu_{c} is the mean of feature x for class c.
% - \sigma_{c}^2 is the variance of feature x for
$$
