
# Graphs 
```python 
graph1 = { "a" : ["d","f"],  
"b" : ["c"],  
"c" : ["b", "c", "d", "e"],  
"d" : ["a", "c"],  
"e" : ["c"],  
"f" : ["a"]}  
  
graph2 = { "a" : ["d","f"],  
"b" : ["c","b"],  
"c" : ["b", "c", "d", "e"],  
"d" : ["a", "c"],  
"e" : ["c"],  
"f" : ["a"]}
```


![[Image.jpeg]]


# 2. BFS 
```python 
  
def bfs(graph):  
	root = list(graph.keys())[0]  
	bfs_queue = [root]  
	visited = []  
	  
	while len(bfs_queue) > 0:  
		# get first node in the queue  
		cur = bfs_queue.pop()  
		  
		for child in graph[cur]:  
			if child not in visited:  
			bfs_queue = [child] + bfs_queue # FIFO ordering  
		  
		if cur not in visited:  
		visited.append(cur)  
	  
	return visited  
  
print("Running BFS:")  
  
print("\ngraph 1: ")  
for node in bfs(graph1):  
	print("-> " + node+" ", end="")  
  
print("\n\ngraph 2: ")  
for node in bfs(graph2):  
	print("-> " + node+" ", end="")
```

### Output 
```
Running BFS:

graph 1: 
-> a -> d -> f -> c -> b -> e 

graph 2: 
-> a -> d -> f -> c -> b -> e 
```

# 3. DFS 
```python 
def dfs(graph):  
	dfs_stack = [list(graph.keys())[0]] # queue will be treated as a stack  
	visited = []  
	  
	while len(dfs_stack) > 0:  
		cur = dfs_stack.pop()  
		  
		for child in graph[cur]:  
			if child not in visited:  
			dfs_stack.append(child)  
			  
			if cur not in visited:  
			visited.append(cur)  
	  
	return visited
```

### Output 
```
Running DFS: 


graph 1: 
-> a -> f -> d -> c -> e -> b 

graph 2: 
-> a -> f -> d -> c -> e -> b 
```

# 4. Advantages and Disadvantages of BFS and DFS

BFS and DFS are similar algorithms and describe the way in which one would visit the nodes in a graph. The advantages of these algorithms depend on the structure of the graph that their being applied to. I think of BFS as the "safer" option since it visits every node at a given level and is guaranteed to find a solution. DFS is a bit riskier with the possible benefit of being more memory efficient. The amount of nodes we have to keep in memory is much smaller than BFS. DFS can get caught in an infinite loop sometimes though and theres no way to guarantee that it will find the optimum solution. 

# 5. Discuss in detail an application of BFS and DFS

**BFS**: BFS is good for the job of route planning. Since it can guarantee an optimum solution, many GPS/Maps services use some version of it to find the optimum route for the user.  This also applies to things like routing data through computer networks in the most efficient way possible. 

**DFS**: one application of DFS is for the task of cycle checking in graphs. If one is able to model a specific problem using a graph, then dfs is good for finding cycles within that graph. For example, when operating systems allocate resources to processes, a graph may be used to track the allocation of resources to certain processes. A cycle in this case represents a possible deadlock point for processes. 