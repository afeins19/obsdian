multiple processes accessing and writing to variables is something that must be managed. 

- Background  
-  The Critical-Section Problem  
- Peterson’s Solution  
- Mutex Locks  
-  Semaphores  
-  Synchronization Hardware  
- Bounded buffer problem  
- Synchronization Examples  

**Example:** video compression algorithms represent  each video frame as an array of 8-pixel by 8-pixel macroblocks. Each macroblock is individually compressed. Performing the macroblock compressions concurrently with a mullti core processor is way to do this quickly


**problem:**  processes can execute concurrently which means that 
- they may be interrupted at any time, including partially during completing execution
- concurrent access to shared data may result in data inconsistency
- maintaining data consistency requires mechanisms to ensure the orderly execution of cooperating processes 

# Race conditions 
two processes trying to perform two conflicting actions simultaneously and the outcome is not predictable. For example, performing the same actions over the same resources. 

![[Screen Shot 2024-02-16 at 10.15.19 AM.png]]

# Critical Sections of Code 
a critical section is a segment of code that is executed by multiple concurrent threads or processes which **access shared resources**. The critical section must be executed as an atomic operation, once one thread or process has entered the critical section, all other threads or processes must **wait until the executing thread or process exits the critical section**. 
- shared memory, files, or other system resources 
![[Screen Shot 2024-02-16 at 10.16.45 AM.png]]

### Developers Role 
this is central to synchronization in computer systems. Note that this responsibility is **not managed by the kernel** it is the role of the **developer** to identify and protect critical sections. 

### Kernels Role
- does not directly manage critical sections
- it provides the underlying mechanisms (mutexes and semaphores)

# Critical Section Problem
consider a system of n processes $\{p_0, p_1, ... p_{n-1}\}$. Each process has a **critical section** of code
- changing common variables, updating tables, writing to files etc. 
- **when one process is in a critical section no other may be in its critical section** 

One must design a protocol that the process can use to synchronize their activities so as to cooperatively share data 
- ex: Mutual Exclusion 
### General Solution Idea
1. **Mutual Exclusion** - if $P_i$ is executing in its critical section, then no other processes can be executing their critical sections
2. **Progress** - if no process is executing in its critical section and there exists some process that wishes to enter their critical section, then the selection of the process that will enter the critical section next cannot be postponed indefinitely 
3. **Bounded Waiting** - without bounded waiting, a process might be indefinitely delayed from accessing a shared resource, leading to unfairness and potentially deadlocks 
![[Screen Shot 2024-02-16 at 10.25.11 AM.png]]
- we define entry and exit sections

### Petersons Solution 
a good algorithmic description of solving the problem, this solution is only applicable to **two processes only** so not very practical

say 2 processes share two variables 
- `int turn` - indicates whose turn it is to enter the critical section (turn based synchronization)
- `boolean flag[2]` - used to indicate if a process is ready to enter the critical section 

![[Screen Shot 2024-02-16 at 10.30.36 AM.png]]
- while loop - the while loop runs when process j is working on the critical section. This blocks process i from working on the critical section until the condition is false. 
![[Screen Shot 2024-02-16 at 10.35.40 AM.png]]

### Why are both turn and flag required? 
if we used turn only, this might lead to either a **race condition** (both processes set turn to their own identifier).

if we use flag only, this might lead to a **deadlock** both processes set their flag to true simultaneously -> indefinite waiting 

### Limitations 
- suitable for only 2 processes 
- busy waiting - process just sits in a while loop while another does a critical section 
- still susceptible to certain race conditions (turn and flag could be modified by other external processes potentially)

# Mutex Locks
Mutual Exclusion Object that provides synchronization services. It is  a synchronization primitive provided by the operating system's **Kernel**. Note that a process must still wait while another process is in its critical section. 
- a specific kind of binary non-negative integer value that is used to provide a locking mechanism 
- mainly used to provide mutual exclusion to a specific portion of the code 

this mechanism is simple to implement and protects a critical section by first doing acquire() and release(). Note that the aquire() and relelase() calls must be **atomic** 
![[Screen Shot 2024-02-16 at 10.45.27 AM.png]]

### Aquire and Release Pseudocode 
![[Screen Shot 2024-02-16 at 10.46.21 AM.png]]

# Semaphore 
In operating Systems, a non-negative integer is shared between threads and **represents the available number resources** that can ensure the safe running of threads. Its used for controlling **how many items** can be produced or consumed concurrently in the **producer and consumer scheme**. 

### Semaphore Atomic Operations
- wait (P)
- signal (V)
![[Screen Shot 2024-02-19 at 10.19.37 AM.png]]
- note that a if we use a binary value to represent the semaphore (0 or 1), this degenerates to a Mutex Lock


###  Example
![[Screen Shot 2024-02-19 at 10.27.47 AM.png]]
there are 6 shared resources and 4 threads. The semaphore is set to 2 denoting that there are 2 available spaces to run threads

### Synchronization
an application of semaphores to order the execution of multiple threads

consider P1 with statements S1 and P2 with statements S2
![[Screen Shot 2024-02-19 at 10.31.42 AM.png]]
- s1 increments synch by 1 
- s2 waits until synch is not 0 to execute 

### No-Busy waiting 
for semaphores to work, we must guarantee that **no 2 processes** can execute the **wait() and signal()** on the same semaphore **at the same time**. This involves having all threads **check** for the resources pool, this uses cpu and is inefficient. No busy waiting solves this issue. 
- with each semaphore there is an associated waiting queue
	- blocking for processes encountering the semaphore count of 0

### Data Structure 
we define a struct with 2 variables 
- `int value`
- `struct process *list`

### Operations 
- block - **places the process** invoking the operation on the appropriate waiting queue 
- wakeup - remove one process in the waiting queue and **place it in the ready queue** 

### Implementation 
![[Screen Shot 2024-02-19 at 10.42.13 AM.png]]say a process calls wait (meaning it wants to run itself) when S<0. This means that there is now a queue of items, this process is then added to the waiting queue and the process is blocked until it is selected. When a process is finished, it calls signal, which increments S. 

Whenever wait is called, we decrement s by 1, so when its back up to zero, we know a process has freed up enough space for at least one process to run. 

### Liveness 
a set of properties that a system must satisfy to **ensure that processes make progress** during their execution life cycle

a **liveness failure** can occur and results in an indefinite wait time such as:
- infinite loops
- deadlocks
- priority inversion 

this can occur when two processes depend on signals on each other to run. But since both processes are waiting, no signal will be sent from either process resulting in deadlock. 

# Limitations of Software Based Synchronization
there are some inherent limitations of software based synchronization solutions. 
- developing and correctly implementing synchronization mechanism may require **careful coding programming practices and thorough testing**
- software based solutions can lead to **deadlocks** when threads or processes are unable to proceed due to cyclic dependencies 
- **performance overhead** - the software for synchronization itself takes computational resources to run

# Hardware Support for Synchronization 

## Memory Barriers 
a synchronization primitive used in concurrent programming to enforce **specific ordering constraints on memory operations**. 
- needed for IPC with shared memory 
- applicable to concurrent threads within the same process

it is a **fence** that separates two sets of operations. ensuring that the ordering constraints are respected. All operations already through the fence are executed first. Once those are done, more operations are allowed past the fence. 

This depends on the on the CPU architecture. For example, intel and and support guarantee that two consecutive load and write operations will occur in the order in which they were issued. 

**Psuedocode:**
```c
// process a
flag = False;

while(!flag){
	memorybarrier();
}

print(x); 
//----------------------------

// process b
x = 100;
memorybarrier();
flag = True; 

x = 100 -> flag=true -> print(100)
```
say these are 2 distinct processes, since process a is going to be printing a value at the memory location x. We need process B to execute first so process A will print something valid (or not error). 

## Hardware Instructions
CPUs that have internal hardware implementations corresponding to specific instructions in their instruction set architecture (ISA). 
- the ISA defines the **set of instructions such as arithmetic, logical, data, movement, and control flow instructions** 

### test_and_set()
it atomically sets a memory location to a specific value and returns its previous value. (this essentially functions like a mutex). 
```c
boolean test_and_set (boolean *target){
	boolean rv *target;
	*target = TRUE;
	return rv;
}
```

Example of test_and_set() 
```c 
#include <stdatomic.h>

atomic_flag lock = ATOMIC_FLAG_INIT;

void acquire_lock() {
    while (atomic_flag_test_and_set(&lock)) {
        // spin-wait (busy wait)
    }
}

void release_lock() {
    atomic_flag_clear(&lock);
}

```
then we can call this function from 2 processes. These 2 processes will share a boolean variable.


### compare_and_swap() 
```c
int compare_and_swap(int *value, int expected, int new_value){
	// note that this is NOT The real implementation, these operations must be done atomically to ensure that only one thread may execute them. 

	// 1. read the current value passed in 
	// 2. comapre the current vallue with expected (old) val
	// 3. If the current val (value) == expected, swap the memory location of *value to the new_vaklue 
	// 4, return a boolean indicating success or failure 

	if(*value == expected){
		*value = new_value;
		return true;
	}

	return false;
}
```

### Atomic Variables 
a tool to provide atomic operations on basic data types such as integers and booleans 
