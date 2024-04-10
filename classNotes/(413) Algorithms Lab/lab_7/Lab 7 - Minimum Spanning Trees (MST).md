# Kruskal's Algorithm

kruskal's algorithm finds the minimum spanning tree by first sorting all of the graphs edges by their path cost and then building up the graph. Sorting the edges by cost guarantees that the next selected edge will have the minimum cost in the entire graph. Before adding an edge to the MST we check to see for the following conditions: 

- any of these edges have been visited before 
- adding this edge would form a cycle in the MST

we do this by building the graph in components. Using a dictionary, I will essentially create a chain from the starting node to the next node that we add to that component of the MST. This lets us make sure that we don't create cycles. 

### Time Complexity 
I will consider the cases of the graph being either sparse or dense 

##### Sparse Graphs
- sorting the edges -> $O(ElogE)$ (python's sort())
- MST Construction:
	-  $O(E \times V)$ 
since E ~ V by some constant we know it grows faster than $O(ElogE)$. For sparse graphs, we can conclude that they have the time complexity
$$O(E \times V)$$
##### Dense Graphs 
For a dense graph with $V$ vertices, we will have $n\times(n-1)$ edges. We can essentially treat this as $|V|^2$ Edges. 

- sorting  the edges -> $O(V^2logV^2) = O(2V^2logV) = O(v^2logV)$
- MST Construction: 
	- using the $O(E \times V)$ but substituting $V^2$ for $E$ we get a time complexity of:
$$O(V^2 \times V) = O(V^3)$$ 
# Prim's Algorithm 

prims algorithm finds a minimum spanning tree with the same cost as Kruskals but does so in a different way. We first pick an initial vertex as a starting point and begin by adding the edge with the lowest path cost from that neighbor to the MST. We continue to do this until we have visited all the vertices in the graph (connected all vertices to the mst).

### Time Complexity

##### Sparse Graphs 
- creating adjacency list: $O(E \times V)$
- MST Construction: $O(E \times V)$ 
so overall we have a time complexity of:
$$O(E \times V)$$
##### Dense Graphs:
- creating adjacency list: $O(V^2)$
- MST Construction: $O(E \times V)$ where $E \rightarrow V^2$ so $O(V^3)$ 
since the MST is the dominating term, we have a time complexity of:
$$O(V^3)$$ 
# Differences Between Kruskal's & Prim's
1. Kruskals will always output the same MST since it looks at the all the edges of the graph first where as prims might produce a different MST since it depends on the starting vertex. However, both algorithms should produce an MST with the same total cost. 
2. Prims Handles Cycles by default whereas Kruskals needs to have cycle detection built into it. 
3. Prims is more efficient for dense graphs where the number of edges is almost the square of the number of verticies. Kruskals would need to first sort all of those edges. Kurskals however is better for sparse graphs where the sorting phase should be linear with the normal efficient sort algorithms 