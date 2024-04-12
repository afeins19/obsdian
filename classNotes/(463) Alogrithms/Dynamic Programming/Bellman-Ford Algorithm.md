note that dijkstras algorithm is not always correct for negative path cost values. Since it is greedy. Negative path costs give rise to issues with finding local minimums but not necessarily global minimums. 

# Single-Source Shortest Path Problem
compute a profitable sequence of financial ltransactions that involves both buying and selling. This problem corresponds to finding a shortest path in a graph with edge lengths that are both positive and negative. 

**input**: a directed graph g = (V,E), a source vertex s in v, and a real-valued length l_e for each edge e in E:

**Output**: 
(i) the shortest-path distance dist(s,v) for every vertex v in V or
(ii) declaration that G contains a negative cycle (and termination without entering an infinite loop)

# The Bellman-Ford Algorithm 
this algorithm solves the single source shortest path problem in graphs with negative edge lengths in the sense that it either computes the correct shortest-path distances or correctly determines that the input graph has a negative cycle. 

If the input graph does not have a negative cycle, subproblem solutions stabilize by the n-th batch. The contrapositive is also true: if an input graph doesn't stabilize by the nth batch, then it has a negative cycle. 

