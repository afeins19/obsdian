# Introduction 
**Idea:** When a package is sent, it must usually transit between shipping hubs and then continue onto a route that eventually delivers it to its destination city and final the end point. Optimum routing is crucial as it saves the company energy, money, and time (which is beneficial for the user as well). 
# Design

## Routing Network (Class)
My data structure will focus on the hub and spoke aspect of parcel services. The routing network will be represented with a graph, with nodes representing intermediate distribution centers. A class representing this network will feature the nodes of the network. Connecting the nodes are edges with path costs corresponding to some cost measure that will be minimized (distance, cost, etc.). 

Large shipping hubs are capable of operating at high volumes have dense connection to the broader network. Path costs to these shipping hubs are usually the cheapest as it is more likely than not that a given node will route to it either directly or vis-a-vi a small number of intermediate nodes. 

I will run MST algorithms such as prims or krushkals to find the MST. This will reduce the complexity of computing the optimum routing for each parcel. 

### Priority
packages sent with a higher tier service will be given priority and will have more rigorous time constraints. I will try to incorporate a queing system to prioritize premium service packages first. This willl involve 
### Attributes 
- Nodes 
- MST 
## Parcel (Class)
Since each package has a unique start and end point, we will need to find the routing corresponding to that specific parcel. Dijkstra's Algorithm will be run to find this optimum routing (minimizing the cost function). 
### Attributes
- unique shipping identifier 
- priority
- strart_vertex
- end_vertex 
- route 

the **route** will be represented with a linked list for fast traversal after it is found. 
## Justification 
The global shipping network is the vital backbone which connects our modern global economy. Efficient, timely, and cost effective distribution solutions allows business to send packages to clients in virtually any part of the world, giving them global reach. The underlying structure that makes this type of operation possible relies on graph theory, algorithmic analysis, and computer science. 

Graph theory provides the foundation on which we can model the distribution network. It is a mature field in mathematics and produce well defined results if the model is used correctly. Algorithmic analysis is vital to ensure that computers can quickly and efficiently find optimum routes for the millions of tons of cargo dispatched each week. I feel that our Data Structures and Algorithms class supplied me with a good tool set to approach this problem. 

