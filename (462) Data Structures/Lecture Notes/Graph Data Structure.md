# Overview

Graphs allow us to represent more connections between nodes and will show where one can travel from any given node 

_Graph_: set of points that are joined by lines
- G = {V, E} 

_Sub-Graph_: Consists of a graph's vertices and a subset of its edges
![[Screen Shot 2023-10-05 at 9.23.11 AM.png]]

*note that all trees are graphs but not visa-versa (tree is a subset of a graph...node may have multiple parents*

# Graph Connections

_Connected_: all vertices have edges
_Disconnected_: some vertices do not have edges
_Complete_: all edges connect to each other

![[Screen Shot 2023-10-05 at 9.26.10 AM.png]]

# Directed Graphs
- edges are ordered pairs (show direction of travel)

![[Screen Shot 2023-10-05 at 9.28.33 AM.png]]

# Multigraph
allows multiple edges between two verticies
![[Screen Shot 2023-10-05 at 9.33.03 AM.png]]
# Psuedograph
a multigraph that allows self-loops (an edge from a vertex to the same vertex)

![[Screen Shot 2023-10-05 at 9.33.29 AM.png]]

# Properties 

- _Simple Path_: a path which passes through a vertex only once
- _Cycle_: a path that begins and ends at the same vertex
- _Simple Cycle_: a simple path that returns to its starting vertex (passing through veracities along path only once)

# Connectivity 

## Strong Connectivity
a graph has strong connectivity if every 2 vertices are reachable from each other

## Weak Connectivity
![[Screen Shot 2023-10-05 at 9.39.01 AM.png]]
*note: if we remove edge (d,e) we wont be able to reach e thus making it weak*

![[Screen Shot 2023-10-05 at 9.38.49 AM.png]]