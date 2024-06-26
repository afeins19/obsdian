greedy algorithm makes the choice that looks best for the current task but it might suffer from focusing on a local min rather than a global min. Dynamic programming explores the space of all possible solutions by carefully decomposing things into a series of subproblems and then building up correct solutions to larger and larger subproblems. 

# Fibonacci Numbers Problem: 
```python
def fib(n):
	if n <= 1:
		return n
	return fib(n-1) + fib(n-2) 
```
note that this implementation is wildly inefficient since we get a time complexity of: $$O(2^n)$$ 
### Optimization
when building the recursion tree, we may end up doing redundant operations for values that we already calculated: 
								fib(5)
								/       \
							fib(4)        fib(3)
							/    \\          /       \
						**fib(3)** **fib(2)**  **fib(2)** fib(1)
if we cache previously calculated fib() values, we can perform an O(1) lookup for its value. this reduces the overall time complexity to a linear value
$$O(n)$$ 
# The Weighted Independent Set Problem
let $G = (V,E)$ be an undirected graph. An independent set of G is a subset $S \in V$ of mutually non-adjacent vercticies $v,w \in S$ such that $(v,w) \notin E$. 

![[Pasted image 20240402122203.png]]


### Brute Force Approach
```
1 - 4 - 5 - 4
```
- { }
- {1}, {4}, {5}, {4}
- {1,5}, {1,4}
- {4,4} -> max independently weighted sets

### Greedy Algorithm Approach (This is the wrong way to go about it)
```
S:= null_set 
sort verticies of V by wheight w 

for each v in V in nonincreasing order of wieght do:
	if S U {v} is an independent set of G then
		S:=S U {v}
return s
```

note that if we run this algorithm on the above graph, ti would see {1,5} and select this. However, the correct answer should be {4,4}. The Greedy algorithm did not find the optimal solution. 

### Divide and Conquer Approach (Also give incorrect results)
```
G1 := first half of G
G2 := second half of G
S1 := recursively solve WIS on G1
S2 := recursively solve WIS on G2 

combine S1,S2 into S 
return S
```
this algorithm would violate the independent set property. It will select {4,5} and although this is the highest sum we could make, it violates our rule set. 

# Linear Time WIS Algorithm 
let S be a MWIS of a path graph G with atleast 2 vertices. Let $G_i$ denote the subgraph of G comprising its first i vertices and (i-1) edges. Then S is either:
- an MWIS of $G_{n-1}$ 
- an MWIS of $G_{n-2}$, supplemented with G's final vertex $v_n$ 

so we either exclude the last element and only consider the preceding elements (first option) or include the last and consider only the nodes at positions (n-2). 

# Recursive WIS Algorithm 
```
if n = 0:
	return the empty set 
if n = 1:
	return {v1}

// consider either case (1) or (2) from the linear algo above and
// recursively solve 
```

Note that this time complexity of this is still exponential as we may only drop a few nodes from our consideration in a level with thousands. 

### Implementation 
```
3 - 2 - 1 - 4 - 5
```
for each index, consider including the items value and the value of the the sum up to (i-2) position (inclusive) and the current node. Select that node and add it to our MWIS. This gaurantees that we will solve each sub problem in the most optimal way. After arriving at the end of the graph we obtain a maximum value for the sum of all elements in the set as well as the position and value for the last node in the set. We must then back track to select the optimum nodes to maximize the sum. This can be done in linear time.

# Knapsack Problem with Dynamic Programming
first divide this problem into subsets and solve the subproblems of those subsets. Let C be the count of items we can carry. Let V be the total value of all items in the subproblem. Starting at 0, solve the following problems for subsets of size |C|. if $S_i <= C$: 

$$V_{i,c} = max(V_{i-1,c}, \; V_{i-1, c-s_i} + V_i)$$
### Represented as as a 2-D matrix
##### Values 

| item | value | size |
| ---- | ----- | ---- |
| 1    | 3     | 4    |
| 2    | 2     | 3    |
| 3    | 4     | 2    |
| 4    | 4     | 3    |

| Items      | cap=0 | 1   | 2   | 3   | 4   | 5   | 6   | $V_{i-1, c-s_i} + V_i$ |
| ---------- | ----- | --- | --- | --- | --- | --- | --- | ---------------------- |
| item=0     | val=0 | 0   | 0   | 0   | 0   | 0   | 0   | 0                      |
| 1          | 0     | 0   | 0   | 0   | 3   | 3   | 3   | 3                      |
| 2 (1,2)    | 0     | 0   | 0   | 2   | 3   | 3   | 3   | 3                      |
| 3(1,2,3)   | 0     | 0   | 4   | 4   | 4   | 6   | 7   | 7                      |
| 4(1,2,3,4) | 0     | 0   | 4   | 4   | 4   | 8   | 8   | 8                      |

- the entries under columns 0,1,2,3... represent the total value gained by adding the value in its row

### Time Complexity of This problem
since we are operating on a 2D array, we need 2 for-loops so well have a time complexity of $O(n^2)$ which is much better than the brute force approach of $O(2^n)$.

### Reconstruction Algorithm
To find the specific items that were used given an overall value. Starting at the largest subproblem, we will try to find which case of the recurrence was used to make the computation - essentially doing the table construction in reverse. This can be done in $O(n)$ time. 

### Total Time Complexity for Both Construction and Reconstruction
$$O(n^2) + O(n) = O(n^2)$$
