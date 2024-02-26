Different process may need to share data with each other for some programs. They need a channel by which to communicate

In general there are two methods of inter process communication (IPC)

# Message passing 
processes communicate with each other without using **shared variables**. this is the safer and more abstracted messaging protocol
- communication is mediated by the kernel
- message passing mechanism include:
	- **pipes**
	- message queues
	- sockets
	- signals

if process *p* and *q* wish to communicate, they need to 
1. establish a communication link
2. exchange messages via send and receive actions 

**design tasks**:
- how are links established?
- can a link be associated with more than two processes? 
- how many links can there be between every pair of communicating processes?
- what is the capacity of a link?
- is there a maximum message size? 
- is the link unidirectional or bidirectional?

## Synchronization 
**Synchronization in Message Passing**
![[Screen Shot 2024-01-29 at 10.41.50 AM.png]]
- **blocking send and receive**
	- both sending and receiving are blocked
	- process A (sender) blocks until process B (receiver) is ready to receive
	- process B (receiver) blocks until Process A (sender) is ready to send 
	- useful when processes need to exchange data simultaneously 

- **blocking send, non-blocking receive**
	- receiving process may continue executing other tasks and periodically check for incoming data but may not block while waiting for data to arrive 
	- suitable when the sender must ensure that data is sent but allows the receiver to perform other tasks in parallel (responsive receiver)
![[Screen Shot 2024-01-29 at 10.46.50 AM.png]]

### Buffering for messages
messages exchanged by communicating processes reside in a temporary queue which is implemented in one of three ways:
1. zero capacity - no messages are queued on a link (sender must wait for receiver (called rendezvous))
2. bounded capacity - finite length of n messages until sender must wait if link is full
3. unbouded capacity - infinite length of messages, sender never waits
### POSIX
portable operating system interface 
- api that defines the cli shells and utility interfaces for software compatibility in unix 
- set of formal descriptions that provide a standard for the design of operating systems, especially ones which are compatible with unix 

![[Screen Shot 2024-01-29 at 10.49.54 AM.png]]
*memory maps are important...look into 'em*

**Example Posix Producer**
![[Screen Shot 2024-01-29 at 10.50.40 AM.png]]

**Example Posix Consumer**
![[Screen Shot 2024-01-29 at 10.50.56 AM.png]]

## Direct Communication 
processes must name each other **explicitly**
- send(p, message) - send a message to process p
- receive(q, message) - receive a message from process q
### Properties of direct communication (logical rather than actual link)
- links are established automatically 
- a links is associated with exactly one pair 
- each link supports exactly **one pair**
- usually bidirectional

## Indirect Communication 
messages are directed and received from **mailboxes**
- each mailbox has a unique id
- mailboxes have unique ids which are specified 
- processes can communicate only if they **share a mailbox**
### mailbox operations
primitive operations are send(B, message) or sending a message to mailbox B or receive(B, message)
- create a new mailbox
- send and receive message through the mailbox
- destroy a mailbox
### properties of indirect communication link (logical rather than actual link)
- link established only if processes share a common mailbox
- a link may be associated with many processes
- each pair of processes may share several communication links 
- links may be uni or bi-directional 

# Shared Memory
	this is a paradigm for cooperating processes, the producer produces information that is consumed by a consumer process 
shared memory allows two or more processes to share a region of memory. **This has higher perfromance but requires careful synchronization**
- processes can be directly read from and write to the shared memory
- the kernel provides mechanisms for processes to **attach to and detach from the shared memory segment**
- synchronization mechanisms like **semaphores or mutexes are required** 

### Shared Memory Protocol
An **unbounded-buffer** places no practical limit on the size of the buffer. An**bounded buffer** assumes that there is a **fixed buffer size**
- producers must **block** if the buffer is full
- consumers must **block** if the buffer is empty 

### Possible issues of Shared Memory 
without proper synchronization, buffers may have the following issues
- the producer doesn't block when the buffer is full
- a consumer consumes an empty slot in the buffer
- two producers write into the same slot
- two consumers read from the same slot 

### Implementation of a bounded buffer 

**Basic Implementation**
```c

#define BUFFER_SIZE 10
typedef struct{
	...
} item;

item buffer[BUFFER_SIZE];
int next_in = 0; // where to write the next data
int next_out = 0; // where to read the next data
```
*this implementation is a correct implementation but we can only use a buffer size of 1*

**Producer Implementation**
```c
item next_produced; /*the item that the producer is going to produce*/  
while (true) {  
/* produce an item in next produced */  
	while (((next_in + 1) % BUFFER_SIZE) == next_out)  
	 ;/* do nothing */  
		buffer[next_in] = next_produced;  
		next_in = (next_in + 1) % BUFFER_SIZE;  
}
```
- the condition ((next_in +1) % buffer_size) == next_out determines whether or not the circular buffer is full after the next write 

**Consumer Implementation**
```c
item next_consumed;  
while (true) {  
	while (next_in == next_out); 
	/* do nothing */  
	next_consumed = buffer[next_out];  
	next_out = (next_out + 1) % BUFFER_SIZE;  
/* consume the item in next consumed */  
}
```
- the condition (next_in == next_out) shows that a producer did not add anything to the buffer so the consumer must wait 

![[Screen Shot 2024-01-29 at 10.23.22 AM.png]]

### Memory Management (shared memory)
an area of memory shared among the processes that wish to communicate 
- this communication is under control of the user processes, not the operating system 
- major issues to resolve: provide a mechanism that will allow the user process to synchronize their actions 

