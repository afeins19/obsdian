# Minimax algorithm
- backtracking algorithm
- used in game theory to find the optimal move for a player
- widely used in turn based games
- we  let p1 -> max and p2 -> min 
- p1 will try to maximize, p2 will try to minimize

![[Screen Shot 2023-09-14 at 12.22.35 PM.png]]

We will use _DFS (Depth First Search)_ to traverse the graph. After all terminal nodes have been observed, we recursively _back-trace_ selecting the best node at each level for the condition of that row {min, max}
- note that this process has a very high  time complexity as we  must visit **each** node!

#  Alpha  -  Beta Pruning 
-  modified  version of Minimax
- optimization technique for minimax 
- prunes  useless branches of minimax tree
- We make the following  definitions:
$$\alpha=max, \beta=min$$


![[Screen Shot 2023-09-14 at 12.46.28 PM.png]]
-  each  row will either be a min or max operation (adversarial gameplay)
- we first start by assigning the nodes directly above the terminal nodes with the left most value (by convention)
- then we compare values based on the  condition of the  row min or max  and replace if needed
- this allows us to visit only the nodes that match the condition and "prune" unneeded ones 