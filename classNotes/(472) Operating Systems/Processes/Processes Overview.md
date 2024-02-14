recall that a **process** is a program in execution. This execution must progress in sequential fashion (the term job and process are interchangeable)

# Parts of a process
- Text section: the program  code
- CPU context: cpu state information such as program counter and register
- Stack: temporary data
	- function parameters, return addresses, local variables
- Data section: global variables
- Heap: memory dynamically allocated during run time

![[Screen Shot 2024-01-24 at 10.18.14 AM.png]]

### Passive Program -> Active Process
- program becomes a process when **executable file is loaded into memory**
- Execution of a program is started via GUI mouse clicks or CLI commands for example  

***note:*** a program may have multiple processes (network requests, GUI listening etc.)

# Process state
- new : process is being created
- running: instructions are being executed
- waiting: process waits for some event to occur
- ready: the process is waiting to be assigned to a processor
- terminated: process has finished execution 

![[Screen Shot 2024-01-24 at 10.20.08 AM.png]]

# Process Control Block (PCB)
	a data structure that contains information about the process (also called a task control block)
**Contains: **
- process state: running, waiting etc.
- program counter: location of next instruction 
- cpu registers: contents of all process-centric registers
- cpu scheduling information: priorities, scheduling queue pointers
- Memory-management information: memory allocated to the process
- Accounting informatio: CPU used, clock time elapsed since start, time limits
- I/o status information: i/o devices allocated to a process 

***note***: the pcb is stored in the os, not in main memory!

![[Screen Shot 2024-01-24 at 10.24.04 AM.png]]

# Threads 
	processes may have more than one thread.
each thread is designated a Thread Control Block (TCB)

![[Screen Shot 2024-01-24 at 10.38.58 AM.png]]

![[Screen Shot 2024-01-24 at 10.39.22 AM.png]]

# Process Scheduling
	to maximize cpu efficiency, we need to maximize cpu use. We need to quickly switch processes on the CPU for time sharing
- process scheduler selects among available processes for next execution on the CPU
- Maintains **scheduling queues** of processes 


### Queueing diagram represents queues, resources, and flows
![[Screen Shot 2024-01-24 at 10.45.21 AM.png]]

### Short Term Scheduler
selects process to be executed next 
- invoked frequently and must be fast 

### Long term scheduler 
selects which processes should be brought into the ready queue
- invoked infrequently
- long-term scheduler controls the degree of multiprogramming 