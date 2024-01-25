implementing the solution
1. identify a free man
2. for man, we need to identify the highest ranked woman to whom he has not yet proposed
3. for a woman w, we need to decide if w is curently engaged
4. Find if the current proposer is more desirable 
# 1. Identifying a free man
### Using a List 
- O(n) time complexity since we may have to do many linear searches over our list of men to find if they are free 

### Better Solution: Linked List
- O(1) time complexity, if a man becomes free, just add them to the head of the list. 

# 2. Identify Next Woman to propose to

### Best Solution: Use a list
	we currently use list to represent the preferences of men. Use another list to serve as a lookup table to quickly find the next woman using O(1) time
- O(1) time complexity 

# 3. Finding if woman is currentely engaged 

### Best Solution
	use a separate list (as a lookup table) to track which current relationships with of the woman. NULL if no current engagement and the man as the value for her current engagemen.
- O(1) time compllexity 

# 4. Determine if current proposer is more desirable 
	before running the algorihtm, create a ranking table (another lookup table) that will rank man m in the sorted order of some woman w's preference 

ex: 
    | m1 | m2 | m3 | m4 | m5
   w1 |   2  |   3  |   1   |   5   |  4
...

we now hold the index directly for the preference of each man resulting in an O(1) lookup 

- O(1) time complexity
