we select a pivot in each stage of sorting where all elements after the pivot are greater and all elements on the left are greater. 

# Overview of Algorithm 
![[Screen Shot 2024-02-08 at 12.15.05 PM.png]]

# Partitioning
![[Screen Shot 2024-02-08 at 12.17.12 PM.png]]
- at each level of recursion we make the array be partitioned properly about the pivot both to the left and to the right 
# Quicksort
![[Screen Shot 2024-02-08 at 12.27.37 PM.png]]
- we then recursively apply quicksort to the left and right sides 
# Benefits of Quicksort
- No extra memory space needed 
- all sorting happens in place 
- recursion happens after partitioning and results dont need to be combined, unlike merge sort 

# Pivot Selection
pivot selection is crucial for optimizing the time complexity of this algorithm. At each sublist, we need the pivot to be the median value of our sublist. This will give us 
$$2*T(\frac{n}{2}) + \Theta(n)$$

where $\Theta(n)$ is the average case time complexity which is $O(nlog_2n)$

###  Expectation value of selecting an index 
$$E = \sum_{i=0}^{n}\frac{1}{n}\times i = \frac{n(n+1)}{2n} = (n+1)/2$$
so on average we pivot equally the left and rgiht sides as n->$\infty$    


#  Time Complexity 
$$T(n) = T(n_1) + T(n_2) + ... $$
where we essentially have $O(n)$ over n elements 

