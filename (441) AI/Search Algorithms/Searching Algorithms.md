
# Depth First Search (DFS)
traverses a graph in a **depth-ward motion** and uses a stack to remember to get the next vertex to start a search. ![[Screen Shot 2023-08-31 at 12.31.37 PM.png]]
(we only have to save a vertex from the previous level in the stack)
## Advantages
- requires little memory as it only stores a stoack of nodes
- takes less time to reach the goal node than BFS algorithm

## Disadvantages 
-  there is no guarantee of finding the solution
- sometimes it may go to the infinite loop 

*note that DFS occupies a lot of memory and time when the solution is at the bottom or end of a tree*

# Breadth First Search (BFS)
traves a graph in a **breadth-ward motion** and uses a queue to remember to get the next vertex to start a search 
![[Screen Shot 2023-08-31 at 12.40.05 PM.png]]

## Advantages 
- provides a solution if any solution exists 
- BFS will provide the minimal solution which requires the least number of steps

## Disadvantages
- requires lots of memory since each level of the tree mist be saved into memory to expand the next level 
- needs lots of time if a solution exists far away 

# Uniform Cost Search 
- a search algorithm used fro traversing a weighted tree or graph when a cost is available for each edge
- the primary goal of the uniform cost search is to find a path to the goal node which has the lowest cumulative cost 
- uniform cost search expands nodes according to their 

## Advantages 
- uniform cost search is optimal because at every state the path with the lowest cost is chosen 

## Disadvantages 
- doesnt care about the number of steps involved in searching and only concerned about the path cost 

# Interactive Deepening Search

![[Screen Shot 2023-08-31 at 12.51.58 PM.png]]
- we must traverse all nodes at a particular level...very time and memory intensive 
- essentially a combination of bfs and dfs

## Advantages 
- combines bfs and dfs 

## Disadvantages
- it is inefficient as the nth iteration requires repeating the traversals from all previous iterations 

# Bidirectional Search 
this search algorithm runs two simultaneous search, one from initial state called forward-search and other goal node called backward-search
- this search replaces a singl search graph with two small subgraphs in which one starts the search from an initial vertex and the other starts from the goal vertex 
- the search stops when these two graphs intersect each other 
## Advantages 
- fast algorithm
- requires less memory 
## Disadvantages
- implementation of bidirectional search tree is hard
- goal state must be known in advance




