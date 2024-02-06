# What is Learning (For Humans)
	we first start with some instructions (or trials) and comes along with conciouss effort to grasp the concept. Eventually this knowledge becomes second nature 

Humans learn from...
- mimicking 
- being informed when one is correct
- experience
- feedback
- comparing certain features 
- analogy
- self-reflection 
### Knowledge
- gained with familiarity through experience or association 
- facts or ideas acquired by study, investigation, observation, or experience 

# What is Machine Learning?
	- How do we extract knowledge from data 
	- How can we automate decisions from data 
	- How can we adapt systems dynamically to enable better user experiences? 

in machine learning, we extract common characteristics (**features**) from the data to gain knowledge. 

Note that instead of creating unique machine learning solutions for each task, we may instead adapt previous implementations 

**Definition of machine learning:** Any process by which a system improves its performance 

### The Role of Statistics
	collected data is processed and then abstracted. The highest level of abstraction for some collection of data is a probability distribution of that data. 

statistics underlies the theoretical portion of machine learning. We can usually always use some statistical methods to describe a process

# Patterns
- supermarket chains collect gigabytes of data from customers every day and may predict who may be likely for a product
### Patterns may help us...
- patterns may help us understand a process
- construct a good and useful approximation 
- account for some part of the data
- detect regularities in the data

# General Machine Learning Algorithm 

![[Screen Shot 2024-01-10 at 1.47.39 PM.png]]
a machine learning algorithm is some function which maps input variables to output variables 

- **Data**: records from the real/cyber world
- **Features:** desired attributes to be extracted 
- **Pattern:** regularities in data (patterns) 
- **Inference**: what can be learnt from these patterns? 
- **Prediction:** what can we predict about this situation 
- **Semantic Labeling:** how can we describe/understand this situation?

# Basic Components of Learning Algorithms
- **representation:** how do you learn and with what?
- **Optimization:** how do you improve?
- **Evaluation:** how did you perform? 

### Methods For the Above:

![[Screen Shot 2024-01-10 at 2.09.16 PM.png]]
# Forms of Machine Learning 
	the main differene between supervised and unsupervised learning is that unsupervised learning methods dont require you to give labeled data, you just give raw data. 
### Supervised
using a series of examples with direct feedback 
### Reinforcement 
Indirect feedback after many examples 
### Unsupervised 
No feedback

### Specific Machine Learning Categories

![[Screen Shot 2024-01-12 at 1.50.17 PM.png]]

# Discriminative & Generative Models 

### Discriminative
	P(Y|X) where X and Y are input and output respectively 
- learn to directly predict the labels from the data 
- learn a boundary (e.g. linear)
- logistic regression, SVM
- **better to predict a label from the data than to model the data**

### Generative
	P(X,Y) or P(X)
- represents both the data and the labels 
- often, makes use of conditional independence 
- Naïve Bayes classifier, Bayesian network 
- **Models of data may apply to future prediction problems**
- **Used for data generation from the learned model**

# Look into Meta-Semi machine learning
