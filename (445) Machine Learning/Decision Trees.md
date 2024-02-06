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

![[Pasted image 20240205141305.png]]


