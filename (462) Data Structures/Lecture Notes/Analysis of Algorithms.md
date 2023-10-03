	instead of directly trying to implement a solution to  a  given problem, its usefull to perform an  algorithmic analysis to find the  most efficient approach. 

_efficiency_ refers to the time and space complexity of the algorithm. We will focus more on the time in this course 

# What  is  an Algorithm
an _algorithm_ is a finite sequence of precise instructions for performing a computation or solving a problem

#  Steps to Create  an Algorithm
1. Understand the problem
2. Design an Algorithm and proper data structures
3. Analyze the Algorithm (Might need to go back to step 2 it too inefficient)
4. Code the  Algorithm

## Considerations
- Capabilities of the computing device
- choose between exact and approximate problem solving

# Algorithm Efficiency
	this is usually expressed in terms of its use of CPU time 
	
_efficiency_: cpu time to run the algorithm
_Problem Size (Pool Size):_ How many elements may be considered 
	- for  search  algorithm this is the search pool

## Growth  Functions
a _growth function_ shows the relationship between the size of the problem set (n) and value optimized (time)

- time complexity  (CPU Time)
- space complexity  (memory space)

## Asymptotic complexity 
this is simply the analysis of our algorithm as (n) increase 

say we have the following  function $$f(n) =  15n^2 + 45n$$
n  = 1 | 15n^2 = 15, 45n =45 
...
n = 1000 | 15n^2 = 1500000 | 45n= 45000

the **dominating term** is 15n^2 so that is  the one that we consider for our algorithm 

## Big-O Notation

![[Screen Shot 2023-09-14 at 9.37.34 AM.png]]

# Divergence of Different Functions

![[Screen Shot 2023-09-14 at 9.40.33 AM.png]]
*note:  cpu power/threads wont help for n with exponential complexity...its  easy to find a large enough n to make the problem intractable*

# Example: For-Loop
-  generally, we analyze the complexity of each for loop and multiply (n) for nested loops and add for separate for loops 
```python
for i in range(100):
	#doing something here
```

assuming the code executed in the for-loop has a constant execution time  

# Constant  Complexity
$$O(100) => O(1)$$

# Linear Complexity
```python
for i in range(n)
	#do something
```
$$O(n)$$

```python
for i in range(n)
	#do something

for j in range(n)
	#do something 
```
$$O(n+n) = O(2n) => O(n)$$
# Quadratic Complexity
```python
for i in range(n):
	for j in range(n)
		#do something
```

$$O(n*n) = O(n^2)$$

##  Example : Find Maximum Value in a Sequence
![[Screen Shot 2023-09-14 at 9.57.05 AM.png]]
*this will take n comparisons to complete*

## Example: Distinct array values
![[Screen Shot 2023-09-14 at 10.02.33 AM.png]]
$$O(n^2)$$

# Hierarchy of Growth  Functions 

![[Screen Shot 2023-09-14 at 10.13.36 AM.png]]

