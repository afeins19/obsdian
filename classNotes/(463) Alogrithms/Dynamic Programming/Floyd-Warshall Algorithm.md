Recall the bellman ford algorithm. It solves a more general problem than dijkstras algorithm (because it can accomodate negative edge costs) 

The drawback with the bellman-ford algorithm is that we must run it n-times to arrive at a conclusion at worst - which is inefficient. The floyd warshall algorithm exploits the fact that the evaluating the recurrence at a vertex v requires information only about vertices directly connected to v 

# Problem: all-pairs of shortest paths 

**Input**: directed graph G = (V,E) with n-vertices and m-edges, and a real-valued length $l_e \; \forall e \in E$. 

**output**: the graph may output one of the following 
1. shortest path distance dist(v,w) for every ordered pair of vertices $(v,w) \in V$
2. a declaration the G contains a negative cycle 

## Sub-Problems
compute the min length of a path in the input graph G (given as $L_{k,v,w}$)that 
1. begins at v
2. ends at w
3. uses only vertices from {1,2,...,k} as internal vertices 
4. does not contain a directed cycle 
(if no such path exists define this path L to be $+ \infty$)  

**Dynamic Programming Update**: The core of the algorithm involves a triple-nested loop (over vertices), where for each pair of vertices (i, j), the algorithm considers whether using another vertex (k) as an intermediate point in the path from i to j can offer a shorter path than currently known. This step is formulated as:
$$dist[i][j]=min(dist[i][j],dist[i][k]+dist[k][j])$$

* The algorithm starts by considering all possible pairs of vertices (i, j), where i and j are the start and end points of the path, respectively. This gives you the n^2 problems, as there are n×n \times n×n combinations of vertex pairs.  For each pair, the algorithm then considers every other vertex k to see if including k in the path between i and j can provide a shorter route than currently known. This is where the n\-times repetition comes in, as each vertex k is considered as an intermediate vertex.

In each iteration of the innermost loop, the algorithm updates the shortest path between the pair (i, j) based on whether the path through k is shorter. By the time all vertices have been considered as potential intermediate steps, the shortest paths between all pairs will have been computed. This systematic approach of solving n^2 subproblems. 

