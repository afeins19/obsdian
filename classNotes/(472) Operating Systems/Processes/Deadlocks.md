a synchronization problem where 2 processes need resources from each other and wait until they are received. This results in an indefinite wait time. 

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

note that having a cycle does not immediately imply that we have a deadlock. **All deadlocks will have a cycle but not all cycles are deadlocks!** 

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
- have some mechanism to recover from deadlock states 
- ignore the problem and pretend that deadlocks never occur (used by most systems including unix)

# Necessary Conditions for Deadlock
to prevent deadlocks, it's necessary to break at least one of these conditions: 
- mutual exclusion
- hold and wait
- no preemption
- circular wait

### Deadlock **Prevention** 
restraining the ways requests can be made so that we may prevent 
- hold and wait
- no preemption
- circular wait

### Mutual Exclusion Prevention
we can reduce mutual exclusion with 
- fine grained locking
- read/write locks (distinguishing between read and write operations) 

### Hold and Wait Prevention
when a process hogs resources and waits until is has all resources it needs. We can prevent this from happening by only running processes that have everything they need to run.
- Require processes to request and be allocated all resources before starting execution 
- once the process has acquired all necessary resources, it can begin its execution without deadlock
- can lead to low resource utilization and delays 
### No-Preemption Prevention 
we can preempt processes that are currently holding resources when resource requested is not available. 
- a process can restart only when resources previously held and previously unavailable when resources are allocated 
- possible starvation due to popular resources being occupied by many different processes frequently 
- applicable to shared resources whose state can be easily saved and restored later like cpu registers and database transactions 
### Circular Wait Prevention
we can impose some ordering scheme for resource usage based on the resource type
- practical solution 
- **impose a total ordering** of all resource types and require that each thread requests resources in an increasing order of enumeration

**Total Ordering:**

define a one-to-one mapping $F: R \rightarrow  \mathbb{N}$    
- A thread can request an instance of resource $R_j$ if and only if $F(R_j) > F(R_i)$where $R_i$ is a resources already assigned  
- each thread must have knowledge of the resources it will need during its execution to make requests on resources in order 
- each thread can request resources only in a n increasing order of enumeration 

**With proper ordeinrg, a circular wait does not exist** 
proof by contradiction: assume a circular wait exists. let the set of threads involved in the circular wait be ${T_0, ..., T_n}$ where $T_i$ is waiting for a resource $R_i$, which is held by thread $T_{i+1}$. Then since thread $T_{i+1}$ is holding resource Ri while requesting resource Ri+1, recall that we have $F(R_i) < F(R_{i+1}) \; \forall i$.
This i a contradiction since this would imply $$F(R_0) < F(R_1) < ... < F(R_n) < F(R_0) \rightarrow \leftarrow $$
# Deadlock Avoidance 
**this is the simplest and most useful model!** 
 ![[Screen Shot 2024-02-26 at 10.48.22 AM.png]]

a method to **dynamically detect and avoid potential deadlocks before they occur**. This is a proactive approach with the potential of wasting some resources. This is different than deadlock **prevention** since prevention is a **static** process where avoidance is a run-time process. 
- dynamically examine the resource allocation state

### Safe State
used for resource allocation decisions. Upon resource request, the system must decide if immediate allocation leaves the system in a safe state. A safe state is defined where there exists a sequence $P_1,...,P_n$ for **all** processes in the system such that $\forall P_i$, the resources that $P_i$ can still request and be satisfied by currently available resources + resource held by all the $P_j$ with j<i. 

if $P_i$ doesn't have all the resources it needs, then $P_i$ can wait until all $P_j$ have finished. if $P_j$ is finished, $P_i$ can obtain needed resources. 

