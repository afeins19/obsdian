# CPU Burst
the amount of time the process uses the processor before it is no longer ready. For maximum cpu utilization and efficiency, we use multiprogramming. 
- varrries from process to process
- long bursts - process is cpu bound (array work)
- short bursts - process i/o bound (vi)
- running processs is moved to the ready state when its time allocation expires 

Histogram of CPU burst times 
![[Screen Shot 2024-02-07 at 10.28.53 AM.png]]

# I/O Burst
the amount of time a process waits for input-output before needing CPI time
- after the i/o burst, the process goes into the ready queue for the next cpu 

# CPU Scheduler 
determines the execution sequence for processes. Processes are moved from the job queue to the ready queue, the cpu scheduler selects from this ready queue and allocates a cpu core to one of them.  
- manages state transitions of processes to ensure efficient sharing of cpu resources among multiple processes or threads in a multitasking environment 
![[Screen Shot 2024-02-07 at 10.35.00 AM.png]]

cpu scheduling decisions may take place when a process
1. switches from running to waiting state
2. switches from running to ready state
3. switches from waiting to ready 
4. terminates 

### Non-preemptive scheduling
once the cpu has been allocated to a process the process keeps the cpu until it releases it either by terminating or by switching to the waiting state 

### Preemptive Scheduling 
cpu allocates limited resources and time to a given process. A process can be interrupted when it is being executed. 
- Better responsiveness is possible
- more overheads due to context switching 

# dispatcher
a module which comes into play after the scheduler. It dispatches the process to the desired state/queue after scheduling. 
- transfers control of the cpu from last process to new selected one
- performs context switch
	- saves the state of outgoing process
	- loading context of new process 
note that **dispatch latency** is a huge factor to consider. Processes with many context switches can slow down the cpu
![[Screen Shot 2024-02-07 at 10.44.13 AM.png]]

# Various Times related to processes
- arrival time - time at which process enters into the ready queue
- burst time - total amount of time required by the cpu to execute the whole process (not including waiting time)
- completion time - time at which the process enters into the completed state or the time at which the process completes its execution 
- turn-around time - total time spent from arrival to completion
- waiting time - total amount of time for which the process waits for the cpu to be assigned
- response time - the difference between the arrival time and the time at which the first process gets selected by the cpu 

# Scheduling Criteria
depending on the criteria, this either becomes a maximization and minimization problem. (max util and throughput, min everything else).
- cpu utilization
- throughput - number of processes that are completed per time unit
- turnaround time - amount of time to execute a particular process
- waiting time - amount of time a process has been waiting in the ready queue 
- response time = amount of time it takes from when a request was submitted until the first response is produced 

# FCFC  (FIFO) Scheduling 

Long burst process arrives first -> average waiting time is quite high 
![[Screen Shot 2024-02-07 at 10.52.12 AM.png]]

suppose now that p2 and p3 arrive first, there is less average waiting time between the processes. 

![[Screen Shot 2024-02-07 at 10.53.10 AM.png]]

### Convoy  Effect
a phenomenon of FCFS scheduling algorithms . A large or resource intensive process ties up system resources and causes a backlog of other processes waiting to use those same resource. 

# Shortest-job-first (SJF) Scheduling 
tries to solve the problem of the convoy effect. It tries to Associate each process with its estimated Burst Times. 

### Determining the length of next CPU burst
![[Screen Shot 2024-02-07 at 10.58.20 AM.png]]
- $\alpha$ determines the number of CPU bursts on average for the previous process. For example $\alpha = 0.1$ means that on average there were 10 bursts. 

### Estimating Process Time 
![[Screen Shot 2024-02-07 at 11.01.05 AM.png]]

