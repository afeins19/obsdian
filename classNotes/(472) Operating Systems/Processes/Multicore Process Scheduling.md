# Symmetric Multiprocessing (SMP)
- each processor is self-scheduling 
- the scheduler for each processor examines the ready queue and selects a thread to run 
- two possible strategies for organizing the threads eligible to be scheduled
		1. all threads may be in a common ready queue -> might result in race conditions on the shared ready queue 
		2. each processor may have its own private queue of threads

![[Screen Shot 2024-02-12 at 10.19.58 AM.png]]

# Multiple Threads on a Single Chip
- recent trend has been to place multiple processor cores on the same physical chip
- faster and consumes less power 
- **multiple threads per core**

### Memory Stall
occurs when the CPU finishes a processor and has to wait for data to be loaded from memory, due it the CPUs faster speed
- multi threaded cores take advantage of this by switching to another thread quickly to work on it while the retrieval happens 
![[Screen Shot 2024-02-12 at 10.22.48 AM.png]]

# Multithreaded Multicore System
each core has more than one hardware thread. If one has a memory stall, switch to another thread! 
- no context switching due to multiple hardware threads
- allowing to use computational resources used for a thread stalled in another thread 

### Chip Multithreading (CMT)
assigns each core multiple hardware threads (intel calls this hyper threading)
- on a quad-core system with 2 hardware threads per core, the operating system sees 8 logical processors 

# Processor affinity 
the association or binding of a software thread (also known as a task or process) to a specific CPU core or set of CPU cores
- performance optimization through minimizing cache misses and improving cache locality 
- efficient resource management through preventing resource contention among threads
- real-time requirements through ensuring that critical threads are executed on dedicated CPU cores with predictable performance characteristics 
- load balancing may affect processor affinity as a thread may be moved from one processor to another to balance loads 

### Soft affinity 
the operating system attempts to keep a thread running on the same processor but does not garuntee it

### hard affinity 
allows a process to specify a set of processors it may run on

### sched_setaffinity(thread_id, pointer) 
this is a function in POSIX. The purpose of this affinity scheduling is to assign tasks for which some cpu cores are specialized in. This allows these cores to better keep context and data in their local cache. 
- accepts the thread_id whose processor affinity you want to set
- a pointer to an array of processor IDS
- **Soft affinity**
	- the thread may run on any processor but is more likely to run on the processors that are specified inits processor affinity mask 


# Real-Time CPU Scheduling
can present obvious challenges such as: 
- soft real-time systems - critical real time tasks have the highest priority but theres no garauntee that they will be scheduled 
- hard real-time systems - task **must** be serviced by its deadline 
- latency is a critical factor in real time scheduling systems 
	- particularly in systems where a timely response to events is essential for meeting performance requirements and ensuring system reliability 

### Event latency
the amount of time that elapses from when an event occurs to when it is serviced 

- **interrupt latency** - time of arrival of interrupt to the start of a routine that the service disrupts
- **dispatch latency** - time for scheduling to take current process off the CPU and switch to another process

![[Screen Shot 2024-02-12 at 10.38.38 AM.png]]

### Interrupt Latency
an interrupt service routine (ISR) is a software routine that hardware invokes in response to some interrupt. ISR looks at the interrupt and determines how to handle it and then returns alogical interrupt value 

![[Screen Shot 2024-02-12 at 10.39.54 AM.png]]

### Dispatch Latency 
there exists a **conflict phase** of dispatch latency - the time it takes to collect the resources from a low priority process 

![[Screen Shot 2024-02-12 at 10.40.48 AM.png]]

# Priority based Scheduling
for any real-time scheduling to work, the scheduler must support **preemptive** priority-based scheduling. However, this only satisfies soft real-time ability. To support hard real-time, we must also have the ability to meet **deadlines**. 

# Periodic Processes 
processes that require the cpu at constant intervals. given a processing time t, deadline d and period p: 
![[Screen Shot 2024-02-12 at 10.47.08 AM.png]]


## Rate Monotonic Scheduling 
- a priority is assigned based on the inverse of tis period 
- shorter periods = higher priority and visa-versa 
![[Screen Shot 2024-02-12 at 10.50.40 AM.png]]

### Missed deadline problem 
its possible for a process to be loaded in where the the execution time might require a time longer than the remaining time left in the period -> missing deadline. This is one issue with using periodic scheduling  

![[Screen Shot 2024-02-12 at 10.52.00 AM.png]]

# Earliest Deadline First Scheduling (EDF)
priorities are assigned according to deadlines. Note that there is overhead as we must spend time on switching contexts and handling interrupts since a new process may be moved in before an old one finishes processing. EDF Considers the deadline as part of the priority. 
- the earlier the deadline, the higher the priority 
- the later the deadline, the lower the priority 

**Example:** ![[Screen Shot 2024-02-12 at 10.55.19 AM.png]]

# Proportional Share Scheduling 
a scheduling algorithm to allocate CPU time among competing processes based on their proportional share of system resources 
- equal wheight is given to every process -> 1/N cpu time to each process where N is the number of processes to be run
- **Dynamic adjustment **- adjusts the allocation of CPU time based on changes in the system load or the arrival of new processes
- **Fairness** - provides fairness in cpu allocation by ensuring that processes receive CPU time in proportion to their weights 