# Introduction 
**Idea:** When a package is sent, it must usually transit between shipping hubs and then continue onto a route that eventually delivers it to its destination city and final the end point. Optimum routing is crucial as it saves the company energy, money, and time (which is beneficial for the user as well). 
# Design

## Overview
my data structure will model a nation-wide shipping network for the US.  
My implementation will feature a graph representing the network. Below  
is the abstraction that is handeld by the graph:  
  
Graph >> ShippingNetwork()  
- Represents the Shipping network  
- uses kruskals to find the mst and store in attribute  
- has a function to run dijkstras for some package given start and end points -> [(hub, pcost), (hub,pcost)...]  
  
Verticies >> hub(city_name, connections)  
- local mail facility where parcels originate or terminate (like ups store)  
- distribution centers (large shipping hub)  
  
Edges >> connections = [(hub, pathcost), (hub,pathcost), ...]  
- shipping time between verticies  
  
Parcel >> Parcel(uniqueId, parcel_weight, origin, destination, dijkstra_path)  
- represents a parcel being sent through the network  
- holds its specific traversal (shipping route)  
  
attributes:  
- uniqueId generator  
- dijkstra_path -> linked list  
- eta (sum of all path costs in its dijkstra path)

## Shipping Network (Class)
My data structure will focus on the hub and spoke aspect of parcel services. The routing network will be represented with a graph, with nodes representing intermediate distribution centers. A class representing this network will feature the nodes of the network. Connecting the nodes are edges with path costs corresponding to the shipping time for which a given parcels route will be minimized. 

Large shipping hubs are capable of operating at high volumes and have dense connections to the broader network. Path costs to these shipping hubs are usually the cheapest as it is more likely than not that a given node will route to it either directly or through a small number of intermediate nodes. 

I will run Krushkal's Algorithm to find the MST. This will reduce the complexity of computing the optimum routing for each parcel. 

```python
class Hub:
    def __init__(self, city_name:str, connections: list):
        self.city_name = city_name
        self.connections = connections
        self.package_count = 0

class ShippingNetwork:
    def __init__(self, hubs: list):
        self.hubs = {h.city_name : h.connections for h in hubs} # all cities in the the network
        self.package_count = 0 # not in use currently
        self.network = self.generate_edges() # makes edges between hubs
        self.mst = None # will hold the mst for the network once all nodes are added

    def __str__(self):
        return str(self.network)

    def generateMst(self): # sets the mst (i will call when all nodes are added)
        self.mst = self.mst_kruskal()

    def addHub(self, hub:Hub):
        if hub in self.hubs.keys():
            return

        self.hubs[hub.city_name] = hub.connections
        self.hubs[hub.city_name].mst = self.mst

    def removeHub(self, city_name:str):
        if city_name not in self.hubs.keys():
            return

        del self.hubs[city_name]

    def remove_loops(self, graph=None):
        """Remove loops from a copy of the shipping network and the processed copy """
        cp_graph = graph if graph else copy.deepcopy(self.hubs) # doesnt actually modify self.nodes

        for hub in cp_graph:  # Use cp_graph instead of self.nodes
            no_loops = []

            for neighbor in cp_graph[hub]:
                if neighbor[0] != hub:  # Check if the neighbor is not the same as the node
                    no_loops.append(neighbor)

            cp_graph[hub] = no_loops

        return cp_graph

    def remove_redundant_paths(self, graph=None):
        """Remove all redundant paths"""
        cp_graph = graph if graph else copy.deepcopy(self.hubs)

        # iterate over nodes
        for hub in self.hubs:
            # dict to hold the cheapest of the duplicate paths (for each node)
            cheapest_paths = {}

            for neighbor, path_cost in self.hubs[hub]:
                # determine if this path cost is cheaper than the currently stored one
                if neighbor in cheapest_paths:
                    if path_cost < cheapest_paths[neighbor]:
                        cheapest_paths[neighbor] = path_cost
                else:
                    cheapest_paths[neighbor] = path_cost

            cp_graph[hub] = [(city, cost) for city, cost in cheapest_paths.items()]

        return cp_graph

    def generate_edges(self, graph=None):
        if graph is None:
            graph = self.hubs  # Default to self.hubs if no graph is provided

        edges = []
        for hub in graph:
            for neighbor in graph[hub]:
                edges.append((hub, neighbor[0], neighbor[1]))  # nodes are tuples of the form (neighbor, path cost)
        return edges

    def getSortedEdges(self, graph=None):
        if graph is None:
            graph = self.hubs  # Default to self.hubs if no graph is provided

        edges = self.generate_edges(graph)
        return sorted(edges, key=lambda path: path[2])

    def mst_kruskal(self):
        # Removing all loops and redundant paths
        processed = self.remove_redundant_paths(self.remove_loops(self.hubs))

        # Generating edges
        processed_edges = self.generate_edges()

        # sort the edges in ascending order
        processed_edges=self.getSortedEdges(processed)


        # Sorting the edges by ascending order
        processed_edges.sort(key=lambda path: path[2])  # Edges are tuples (node_1, node_2, path cost)
        #print(processed_edges)

        # Connect the nodes together, store each node in a visited list to ensure that we don't add it again
        visited = []
        mst = []

        for tup in processed_edges:
            ns, ne, pc = tup

            if ns not in visited or ne not in visited:
                mst.append(tup)

                visited.extend([ns, ne])

            if len(visited) == len(self.hubs):  # Fix here, use self.nodes instead of processed.nodes
                break  # Stop when all nodes are visited

        # format the mst to the same way as self.hubs so we can run dijkstras later
        mst_graph = {hub: [] for hub in self.hubs}

        # fill mst with edges (undirected so well make links from nodea to nodeb and reverse)
        for start, end, cost in mst:
            mst_graph[start].append((end, cost))
            mst_graph[end].append((start, cost))  # Assuming undirected graph

        return mst_graph

    def findOptimumParcelRoute(self, start=None, end=None):
        """Dijkstra's algorithm without priority queue:
            1. Mark all nodes as unvisited and put them into an unvisited set.
            2. Assign every node a tentative distance value (set to infinity for unvisited nodes and 0 for the initial node).
            3. Set the initial node as the current node.
            4. For the current node, consider all unvisited neighbors and calculate their tentative distances through the current node and assign.
               - If the distance was marked previously with a longer path, change it to the shortest one that's now found.
            5. If the destination node has been found OR the unvisited set is empty, HALT.

            New Modifications:
                - returns the entire path not just the (vertex, pathcost) tuple for each vertex
        """
        # hubs passed in?
        if not start or not end:
            return None

        # hubs exist?
        if not start in self.hubs and not end in self.hubs:
            return None

        # mst generated?
        if not self.mst:
            return None

        if start not in self.mst or end not in self.mst:
            return None, float('infinity')  # Return if start or end is not in MST

        distances = {hub: float('infinity') for hub in self.mst}
        distances[start] = 0
        predecessors = {hub: None for hub in self.mst}

        unvisited = set(self.mst.keys())

        while unvisited:
            current = min(unvisited, key=lambda hub: distances[hub])

            if distances[current] == float('infinity'):
                break  # cant reach

            unvisited.remove(current)

            for neighbor, path_cost in self.mst[current]:
                new_distance = distances[current] + path_cost
                if new_distance < distances[neighbor]:
                    distances[neighbor] = new_distance
                    predecessors[neighbor] = current

        # Reconstruct the path
        path = []
        current = end
        while current is not None: # starts with the end node and works backwards by quering dict with the city names for the previous pair
            path.insert(0, current)
            current = predecessors[current]

        if path[0] != start:  # Check if the start node is the first in the path
            return None, float('infinity')  # No path found

        return path, distances[end]


```
## Parcel (Class)
Since each package has a unique start and end point, we will need to find the routing corresponding to that specific parcel. Dijkstra's Algorithm will be run to find this optimum routing (minimizing the cost function). Each Parcel will have its unique path, uniqueId (a class variable that gets incremented) and an eta (the sum of the combined path costs from start to end).
### Attributes
- unique shipping identifier 
- priority
- strart_vertex
- end_vertex 
- mst
- dijkastra_path

```python
class Parcel:
    uniqueIdCounter = 0

    def __init__(self, origin, destination, weight, uniqueId=None):
        # class variable to create unique parcel ids
        Parcel.uniqueIdCounter += 1

        self.uniqueId = Parcel.uniqueIdCounter + 1
        self.origin = origin
        self.destination = destination
        self.weight = weight
        self.dijkstra_path = None
        self.eta = 0

        # recieves mst from shipping network parcel is added to the network
        self.mst = None

    def setMst(self, mst):
        self.mst = mst

    def assignRoute(self):
        route, total_cost = us_network.findOptimumParcelRoute(self.origin, self.destination)
        self.dijkstra_path = route
        self.eta = total_cost

    def __str__(self):
        return f"ID: parcel_{self.uniqueId}| {self.dijkstra_path[0]} -> {self.dijkstra_path[-1]} | ETA={self.eta} | path={self.dijkstra_path}"
```

the **route** will be represented with a list after it is found. 
## Conclusion & Justification 
The global shipping network is the vital backbone which connects our modern global economy. Efficient, timely, and cost effective distribution solutions allows business to send packages to clients in virtually any part of the world, giving them global reach. The underlying structure that makes this type of operation possible relies on graph theory, algorithmic analysis, and computer science. 

Graph theory provides the foundation on which we can model the distribution network. It is a mature field in mathematics and produces well defined results if the model is used correctly. Algorithmic analysis is vital to ensure that computers can quickly and efficiently find optimum routes for the millions of tons of cargo dispatched each week. I feel that our Data Structures and Algorithms class supplied me with a good tool set to approach this problem. 
