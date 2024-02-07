machine learning algorithms are based on the tree structure
- starts at root and branches off
- flowchart-like operation 
	- starts a the root node with a specific question about the data
	- each branch leads to a potential answer/approach
	- the branches then lead to decision (internal nodes) which ask more questions to narrow it down 
![[Pasted image 20240205140234.png]]

this is an effective method for making decisions
- lay out the problem and all possible outcomes


## Trees terminology in ml
- root - represents entire message or decision
- decision (internal) node - a node where the prior node branched into one of two variables
- leaf (terminal) node - 
- splitting - the process of dividing a node into two or more nodes 
- pruning - the opposite of splitting, the process of going through and reducing the tree to only the most important nodes or outcomes 


# Classification Trees
tree to classify -> arrive at a specific output

# Regression Trees
algorithms to predict what is likely to happen given some information
- example: housing prices in Colorado
	- input - what prices have been in previous years
	- output - house prices in the next year 


# Construction of a Decision Tree
1. select an attribute to place at the root node and make one branch for each possible value
2. split up the example set into subsets, one for each 
	...

# Examples
![[Pasted image 20240205141153.png]]

### how to determine which attribute to split on
- any leaf with only one class will not have to be split futrther
- a measure of purity of each node may be useful
	- information in the unit of bits
	- the expected amount of information that would be needed to describe information 
![[Screen Shot 2024-02-07 at 1.39.51 PM.png]]
![[Screen Shot 2024-02-07 at 1.39.38 PM.png]]

![[Screen Shot 2024-02-07 at 1.47.08 PM.png]]
# Limitation of information gain 
accroding to this rule, we ought to select the root node with the most children (most information gained from a node). However, some attributes are not relavent to our particular decision and we may may go down a root node with many children that doesn't help us at all with our problem

# The Gain Ratio 
tries to counter the information gain problem by taking into account for the issues with information gain 
- taking into account the number and size of daughter nodes 
- calculated by dividing the original information gain by the uncertainty of the attribute 
### Issue with information gain

![[Screen Shot 2024-02-07 at 1.47.54 PM.png]]

# ID3 
a top down greedy search algorithm. We replace information gain with a **standard deviation reduction** strategy. The idea is to partition the data into subsets that contain instances with similar values (homogeneous). 
- standard deviation (s) -> branching 
- Coefficient of Deviation (CV) or Count (n) -> stop branching 
### Standard deviation for one attribute 
![[Screen Shot 2024-02-07 at 1.52.36 PM.png]]
- we do this to scale the so one homogenous group doesn't dominate another based on the magnitude of the values of that happen to be in a particular group 

### Calculating Std. Deviation for 2 attributes 
$$S(T,X) = \sum{P(c)S(c)}$$

![[Screen Shot 2024-02-07 at 1.57.22 PM.png]]

### Std. Deviation Reduction Technique 
based on the **decrease in standard deviation after a dataset is split** based on an attribute. 

![[Screen Shot 2024-02-07 at 2.00.17 PM.png]]

![[Screen Shot 2024-02-07 at 2.00.26 PM.png]]

![[Screen Shot 2024-02-07 at 2.00.36 PM.png]]

![[Screen Shot 2024-02-07 at 2.00.48 PM.png]]

![[Screen Shot 2024-02-07 at 2.00.59 PM.png]]

![[Screen Shot 2024-02-07 at 2.01.14 PM.png]]
![[Screen Shot 2024-02-07 at 2.01.27 PM.png]]
![[Screen Shot 2024-02-07 at 2.01.55 PM.png]]



