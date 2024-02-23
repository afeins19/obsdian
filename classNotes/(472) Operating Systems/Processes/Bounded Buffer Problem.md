the problem of **coordinating interactions between producer and consumer processes** that **share a fixed buffer size**
- ensure that producer doesn't overflow 
- ensuring that consumer doesn't underflow 

To solve this we do define 3 semaphores that are shared between the producer and the consumer
- int n (number of elements)
- semaphore mutex = 1 (binary mutex) - updates next_in and next_out
- semaphore empty = n (initialized to n since at start all memory slots are empty) - counts the number of empty slots in the buffer 
- semaphore data = 0 (no data slots so 0 at start) - counts number of data items in the buffer 

### Pseudocode for Bounded Buffer 

**Producer Code**
```c
do { 
	/* produce an item in next_produced */
	wait(empty); // wait if buffer is full (empty is 0)

	wait(mutex); // then wait until no other critical section is being executed

/ * add next_produced to the buffer */
signal(mutex); // release the lock on the critical section
signal(data); // signal that the buffer is no longer empty

} while (true)... 
```

**Consumer Code**
```c
do { 
	/* Consume an item in next_produced */
	wait(empty); // wait if buffer is full (empty is 0)

	wait(mutex); // then wait until no other critical section is being executed

/ * add next_produced to the buffer */
signal(mutex); // release the lock on the critical section
signal(data); // signal that the buffer is no longer empty

} while (true)... 
```



