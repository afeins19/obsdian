given an undirected or directed G = (V,E) starting from any vertex s $s \in v$. 

a graph may have a minimum 2 layers (a tree of 1 parent node and (n-1) child nodes) or n layers (a vertical linked list of nodes). 

# Shortest Path 
with just a few extra lines of code added to BFS, we an efficiently compute shortest-path distances.

In graph G we use dist(v,w) to represent the fewest number of edges in a path from v to w. or (+inf if G has no path from v to w).

- initialize the shortest path distance to 0 for the start vertex
- set all other vertices to +inf
- For each neighbor of the current node, add the distance until the current node from star +1 as the distance from start to that niehgbor 

### Time Complexity 
$O(n+m)$ | m = number of edges, n = number of verticies 

# Computing Connected Components of a Graph (UCC Algorithm)
a connected component is a maximal subset s of all the V verticies such that there is a path from any vertex in S to any other vertex in S 

we may have at least 1 connected components up to a maximum of n connected components for a graph G with n elements (n>=1). 


![[Screen Shot 2024-02-27 at 1.02.24 PM.png]]


