0![[Pasted image 20240418121908.png]]
if there is a salesman trying to visit every city, find the most efficient path for him to take (minimize). 
$$g(i,S) = min_{k \in S}(C_{ik} + g(k, S- \{k\}))$$

- g = cost function
- i = starting vertex
- k = current location
- s = remaining vertices 

# Brute Force 
in general for n-cities we have a total number of unique paths equaling: $$(n-1)!$$
- 6 cities -> 5! = 120
- 30 cities -> 29! ~= 10^55 
heckin mucho...

# Greedy Approach 
although in this example the greedy algorithm solution is the most efficient, it is **not guaranteed to provide the global optimum**. 

# Dynamic Approach 

![[Screen Shot 2024-04-18 at 12.47.07 PM.png]]we can cache the solutions for previously solved problems to perform $O(1)$ lookups on them later. 

# Generate all Possible Subsets of the Vertices 
for example, for nodes 1,2,3 we have the following subsets. This represents the number of problems that must be solved

| # elements |                   |     |
| ---------- | ----------------- | --- |
| 0          | nullset           |     |
| 1          | {1},{2},{3}       |     |
| 2          | {1,2},{1,3},{2,3} |     |
| 3          | {1,2,3}           |     |

# BellmanHeldKarp Algorithm
![[Screen Shot 2024-04-18 at 12.52.21 PM.png]]