Say we have an array of values that should be ordered in increasing order 
$$a = [1,3,5,2,4,6]$$
inversion pairs are those that are in the correct order relative to each other.

**inverted pairs**
$$(5,2), (5,4), (3,2)$$
we want to find an algorithm that will calculate this number of inversions. Note that every array that is not sorted has at least one inversion. 

# Collaborative Filtering Problem 
to compute a numerical similarity measure that quantifies how close **two ranked** lists are to each other
- ranking movies to find out if two people have similar preference
- if the rankings are identical, the arrays will be sorted and have no inversions
- the more inversions the array has, the greater the difference in preference 

The maximum number of pair-wise inversions 
$$n\choose2$$ where n is the size of the list. 

# Movie Ranking Problem
how do we find out how similar these two lists are to each other. The idea is to find how many inversions exist between A and B. 
![[Screen Shot 2024-01-30 at 12.21.04 PM.png]]
- *customer A* ranks the movies in such a way
- *customer B* ranks the movies in his way 

## Brute Force Approach
![[Screen Shot 2024-01-30 at 12.25.34 PM.png]]

### Big-O
- if statement => constant O(C)
- inner for loop => O(n)
	- $$n-(n-1) + n - (n-2) + ... + (n-1)$$
- outer foor lop => O(n)
**total** 
$$O(n*n+c) = O(n^2)$$
not ideal :(

### Divide and Conquer Approach 
we can apply a technique thats similar to merge sort to reduce this time complexity. Use split functionality of merge sort to divide the list into sublists of length (n/2). when we arrive at the base case (lists of length 1), every time we need to select an element from the opposite list of the one were checking, this indicates an inversion and must be counted. 

we must also check for **split inversions** when there exist inversions between 2 lists that dont have inversions within them but inversions exist between the 2 lists.

![[Screen Shot 2024-01-30 at 12.35.01 PM.png]]
- we essentially add the number of inversions in each sublist and the number of inversions in split lists. 
- then we return the sum of all three types of inversions 
### Question
![[Screen Shot 2024-01-30 at 12.39.39 PM.png]]
- (B) since there is no split inversion detected, that means that all values in C are ordered correctly relative to numbers in D, so all elements in C are less than all elements in D 

### Optimized Approach
![[Screen Shot 2024-01-30 at 12.44.59 PM.png]]
note that at each level of merging, all sublists are sorted internally => no split inversions. When we reach a point where a value in the right sublist is less than the left sublist, we know that this value will be less than **all remaining*** values in the left subarray (since its sorted). 

![[Screen Shot 2024-01-30 at 12.47.01 PM.png]]

### Running Time
This is a merge sort technique which has O(nlogn) + c where c is the additional if statement check that we apply. we still have $$O(nlogn)$$
