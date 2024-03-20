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

### Resource Allocation Graph Scheme
- a **claim edge** $P_i -> R_j$ indicates that process $P_i$ may request $R_j$ (given by a dashed line)
- a claim edge converts to a request edges when a process request a resource 
- when a resource is released by a process, the assignment edge converts back to a claim edge 

# Bankers Algorithm 
a resource allocation and deadlock avoidance scheme to decide whether or not to approve a request for a resource to an individual process or not in systems with multiple instances of resource types
- multiple instances 
- each process must provide an **a priori claim of maximum use** 
- when a process requests a resource, it may have to wait 
- when a process gets all its resources it must return them in a finite amount of time 
- composed of a **safety algorithm** for the existence of a sequence and a resource** request algorithm** for checking strict conditions for resource allocation 
### Safety Algorithm 
- runs periodically or as needed by the operating system to check the current system state for safety 
- proactively assess whether the current allocation of resources allows for the existence of a safe sequence of processes

**Algorithm**:
1. let work and finish be vectors of length m and n with work[j] = available[j] and finish[i] = false for all i,j
2. find a process i such that both:
	1. finish[i] = false 
	2. need[i,j] <= work[i,j] for all 0<=j<=m. if no such i exists to satisfy this condition, go to step 4 
	3. conceptually execute process i and finish[i] = true and release its resources (since resource occupied by process i is now available so work[j] = work[j] + allocation[i,j] for all 0<=j<=m)
	4. if Finish[i] == true for all i, then the system is in a safe state 
### Resource Request Algorithm 
- run in response to a specific resource request made by a process
- first check safety for potential allocation with a safety algorithm 
- second, allocate the resource if it keeps the safe state of the system 

### Implementation of Bankers Algorithm 
**Data Structures:**
- n = number of processs 
- m = number of resource types 
- available = vector of length  m
	- i.e. available[j] = k -> instances of resource type R_j
- Max = an n x m matrix that represents max resource usage by each process 
	- Max[i,j] = k -> process P_1 may request at most k instances of resource R_j
- Allocation = n x m matrix representing the current resource assignment 
	- allocation[i,j] =k -> P_i may need more instances of R_j to complete its task 
	- Need = Max - Allocation 

**Safety Algorithm**
we can find the status of a being in a safe state or not by simulating the allocation of resources to processes in a way that ensures that all processes can eventually complete their execution without getting stuck in a deadlock. 
- the algorithm tries to find a sequence of allocations that avoids resource contention and ensures system safety 
- **it does not try full search**
- it usually tries a nested for loop

```python 
for _ in range(num_processses):
	# iterate over starting process 
	for i in range(num_processes):
		# iterate over possible resource allocations 
```

### Allocation Matrix 
used for several instances of a given resource type
- **available:** a vector of length m indicating the number of resources of each type
- **allocaiton:** an n x m matrix defines the number of resources allocated to each process already
- **request:** an n x m matrix indicates the current request of each  
process. If `Request [i][j]` = k, then process $P_i$ is requesting k more  
instances of resource type $R_j$

![[Screen Shot 2024-03-11 at 10.24.31 AM.png]]![[Screen Shot 2024-03-11 at 10.24.47 AM.png]]

### Example of deadlock detection with allocation matrix![[Screen Shot 2024-03-11 at 10.25.15 AM.png]]

### Process Abortion
processes can be aborted as a way of breaking deadlocks. We may either abort all processes (an inefficient and disruptive method) or we can abort one process at a time until the deadlock cycle is eliminated 

### Resource Preemption
successively preempt some resources from processes and give these resources to other processes until the deadlock cycle is broken
- select a victim process (one with the lowest cost)
- rollback - return to a safe state - restart that process