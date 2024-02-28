The POSIX.1b standard is an api that provides functions for managing real-time threads

# SCHED_FIFO 
threads are scheduled based on their arrival order and priority. Threads with higher priority preempt threads with lower priority, but within threads of the same priority. The scheduling is based on the **order of arrival in the ready queue** 

# SCHED_RR
similar to SCHED_FIFO except **time slicing** occurs for threads of equal priority 

# Scheduling Algorithm Evaluation Techniques
### Deterministic Modeling
a type of analytic evaluation. takes a particular predetermined workload and defines the performance of each algorithm for that workload. 

Consider 5 processes arriving at time 0:
![[Screen Shot 2024-02-14 at 10.17.55 AM.png]]

for each algorithm, calculate the minimum average waiting time. This is a fast technique but requires exact values for input and applies only to those specific values 
### Queueing Models
describes the arrival of processes and CPU and i/o bursts probabilistically 
- commonly exponential and described by the mean 
- computers average throughput, utilization, waiting time etc. 
computer system is described as a network of servers, each with a queue of processes waiting to be run
- knowing arrival rates and service rates
- computes utilization, average queue length, average wait time, etc. 

![[Screen Shot 2024-02-14 at 10.21.41 AM.png]]


##### Littles Formula
based on littles law - in a steady state, processes leaving the queue must equal processes arriving into the queue
- L = average queue length
- W = average waiting time in queue
- $\lambda$ = average arrival rate into queue 

based on littles law and the steady state assumption we get:
$$L = \lambda \times W$$
this is valid for any scheduling algorithm and arrival distribution 

# Simulations
- tries to address queueing modells limitations
- simulations can be more accurate
	- programmed model of a computer system
	- clock is variable
- **lets you gather statistics indicating algorithm perofrmance**
- data to drive simulation is gathered via
	- random number generator according to probabilities 
	- distributions defined mathematically or empirically
	- trace tapes record sequences of real events in real systems
![[Screen Shot 2024-02-14 at 10.26.14 AM.png]]

# Direct Implementation
just implement the scheduling algorithm and test it directly, this is a high cost and high risk procedure though and takes time to setup for an environment. Most flexible schedulers can be modified per site or per system
- use APIs to modify priorities 
- Environments vary 
