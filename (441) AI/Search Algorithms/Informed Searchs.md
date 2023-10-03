	the algorithm contains an array of knowledge such as how far we are from the goal, path cost, how to reach a goal node, etc. This knowledge helps agents to explore less of the search space and find the goal node more efficiently. The informed search algorithm is more useful for a **large search space** 

# Difference from Uninformed Cost Searches
- Uninformed cost searches expand nodes only by the cost of their path
	- this is done by some sort of evaluation function which returns the cheapest path from the current node to a neighbor
- Crucially, **Uninformed searches do not take into account the cost of the entire path**
	- the cheapest edge from the current node to a neighbor may actually be leading the us away from a goal state

# Best First Searches
	uses an evaluation function to find the cheapest node to expand (f(n) = h(n) where g(n) is the cost of the path from the current node to the goal node)

Step-1: Place the starting node into the OPEN list.  

Step-2: If the OPEN list is empty, Stop and return failure.  

Step-3: Remove the node n, from the OPEN list which has the  
lowest value of h(n), and place it in the CLOSED list.  

Step-4: Expand the node n, and generate the successors of node  
n.  

Step-5: Check each successor of node n, and find whether any  
node is a goal node or not. If any successor node is goal node,  
then return success and terminate the search, else proceed to  
Step-6.  

Step-6: For each successor node, algorithm checks for evaluation  
function f(n), and then check if the node has been in either OPEN  
or CLOSED list. If the node has not been in both list, then add it to  
the OPEN list.  

Step-7: Return to Step-2.

## Possible Implementation
```python
from queue import PriorityQueue

v = 14
graph = [[] for i in range(v)]

def best_first_search(start, end, graph_size):
	#first we enumerate how many visited nodes are possible
	visited = [False] * n
	#next we create a priority queue
	pq = PriorityQueue()
	#we then insert our starting point giving it priority
	pq.put((0, start))
	#lastly we will mark our nodes index in the visited list
	visited[start] = True 

	while pq.empty() == False:
		node = pq.get()[1]
```
### Advantages
- best-first searching allows us to use a hybrid of bfs and dfs and "chooses" the approach to use at each node 

### Disadvantages
- may result in infinite loop
- may expand nodes that are cheap to reach but doesn't care whether or not they move us closer to goal states
## Heuristic Functions
	problem-specific evaluation function which informed algorithms use to prioritize nodes. These could be anything as each problem will have its own heuristic for tracking progress towards goal states 

$$h(n)$$
- the only constraint is that h(n) = 0 for the goal state 
## Greedy Search Algorithm
	the greedy search algorithm expands nodes based on a huerisitic function which choose to expand nodes with the lowest cost to the goal from the current node (denoted h(n)).

### Advantages
- if we have a good heuristic function, this search is quite fast and memory efficient
### Disadvantages
- if it turns out that there exists a path to a node that was already visited, Greedy-Search **will not** take this into account 
- remember, it only tries to minimize the cost to reach the goal from the **current node**

## A* Search
	A* search is similar to greedy-search but improves upon it by also considering the cost of the path from the start node to the current node. it is a combination of uniform-cost search (considers the cost to reach the next node) and greedy-search (considers the cost to reach a goal state from the current node)

### Heuristic Function for A*
	In order to consider both h(n) (cost to the goal from the current node) and g(n) (the total to the current node from the start node) its acctually just the summation of both functions

_A* Heuristic_
$$f(n) = h(n) + g(n)$$

### Advantages
- A* algorithm is optimal 

## Examples for A* 

Let G = no. steps to be taken to reach current state 
Let H = estimated distance 

**f(x) = g(x) + h(x)**


| 1 | 2 |   |  
| -------- | -------- | -------- |  
|  4 |  5 |  3 |  
| 7 |  8 |  6 |

# Cost Calculation (for a single possible move)

| 3 | 2 |  8 |  
| -------- | -------- | -------- |  
|  4 |  5 |  6 |  
| 7 |  1 |   |

**this is the cost of moving each item to its correct square**

8: h = 3
7: h = 0
6: h = 0
5: h =0 
4: h = 0
3: h =2 
2: h = 0
1: h = 3
	total: 8 

select branches which yield the lowest cost function output

we then repeat this process continuously 

# Goal State Checking
- the goal is to have our board match the goal state board
	- our function needs to check if a given move brings us closer to a goal