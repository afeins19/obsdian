# Search algorithms

Search Algorithms Try to traverse a space in the most efficient possible way. Problems with redundant paths (Even simple ones) can generate insane amounts of nodes when step count is increased. (a rectangular grid of 4 nodes has 4^d possible leaves (with only 2d^2) distinct ones). If d = 20, there are over 1 trillion nodes but only about 800 distinct states.  

# Tree  search
	A simple algorithm where nodes are appended to the frontier or open list. each time a new node is discovered its children are added to the frontier. 

# Graph search 
	graph search expands upon tree search by augmenting it with an explored set (or closed list). If a node that is  currently being observed already exists in the frontier or expanded list, it will discarded.
- if the successor to a node is already explored, we stop exploring the node 
![[Screen Shot 2023-09-11 at 1.12.41 PM.png]]







