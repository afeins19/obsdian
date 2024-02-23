a synchronization problem where 2 processes need resources with each other and wait until they are received. This results in an indefinite wait time. 

# System Model 
a system is modeled in the following way. We have m-resources (R). Each resource type $R_i$  has $W_i$ instances. 
$$R_1, R_2, ..., R_m$$
### Resource Util Process
- request for resource
- use of resource
- release of resource

### Deadlock Example 
each thread locks the mutex for the other thread and visa-versa 
![[Screen Shot 2024-02-23 at 10.39.51 AM.png]]
*note the arrows, there appears to be **cycle** through the diagram*. 


# Resource Allocation Graph
we can use graph theory to model the deadlock process. **a cycle is necessary but insufficient to prove that we have a deadlock.**
![[Screen Shot 2024-02-23 at 10.43.43 AM.png]]

### Verticies (V)
verticies are partitioned into two types 
- P - processes
- R - resources 

### Edges (E)
- request - directed edge
- assignment - directed edge 


### Example of Resource Allocation Graph Cycle

![[Screen Shot 2024-02-23 at 10.45.11 AM.png]]
- p1 requests r1, but r1 is assigned to p2
- p2 requests r3, but r3 is assigned to p3 
- p3 requests r2, but r2 is already assigned to p1 and p2 
there is no way for any process to get their requested resources. All the resource are currently occupied and all process are waiting for their resource so we have a **Deadlock**. 

note that having a cycle does not immediatly imply that we have a deadlock. **All deadlocks will have a cycle but not all cycles are deadlocks!** 

![[Screen Shot 2024-02-23 at 10.50.43 AM.png]]

# Circular Wait 
a circular wait is a set $P_0, P_1, ..., P_n$ where 
- $P_0$ waits for a resource held by $P_1$
- $P_1$ waits for a resource held by $P_2$
- $P_{n-1}$ waits for a resource held by $P_n$
- $P_n$ waits for a resource held by $P_0$

# Deadlock Handing 
ensureing that the system will never enter a deadlock state. This is the job of the **software engineer**.  We can **prevent** the issue using software design, and also avoid it at **runtime** with runtime checks. 

### Possible Approaches 
- have some mechanism to enter a deadlock state and then recover
- ignore the problem and pretend that deadlocks never occur (used by most systems including unix)
