the idea of virtual memory is based on the concept that the entire program does not need to be in memory to run the program, we only need to execute a **partially-loaded** program - just enough space to run the current processes of the program. This  takes less memory. This allows us to load programs that are larger than the memory size available. 

### Overview
virtual memory is a technique that provides an abstraction of the computers physical memory 
- logical address space can therefore be much larger than physical address space
- only part of the program needs to be in memory for execution
	- dynamically loaded parts of a program are typically loaded into main memory
	- the rest of the program may reside in the virtual memory region 
	- less i/o is needed to load or swap processes 

# Implementation 
can be implemented via 
- demand paging
- demand segmentation

more programs can run concurrently and virtual memory is larger than physical memory 


# Demand Paging 
a memory management technique used by the OS to efficiently manage RAM and virtual memory 
- managed by memory management subsystem in kernel

a memory management of loading the required pages of a program into memory only when it is needed. Pages are only loaded when they are demanded 

### Valid and Invalid Bits
- v => indicates that page is in memory 
- i => indicates that page is not in memory 
- this bit is initialized with i on all entries at the start 
if the MMU requests a page with this bit set to 'i', this results in a **page fault**

### Page Fault 
an event where a program attempts to access data o code that is not currently located in the system RAM. This requires invoking the page fault **handling procedure**. 

1. To resolve page faults the operating system checks two things:
	-  the current memory reference is invalid -> abort the program 
	-  the required data is not in main memory -> requested page is in secondary memory 
2. find a free frame
3. swap page into frame
4. reset tables to indicate page is now in memory and set validation bit to 'v'
5. restart the instruction that was interrupted

##### Pure demand paging
only bringing processes into memory when they are required. Might increase efficiency but also incurs high risk of page faults 

### Effective Access Time (EAT)
 where p is the probability of a page fault. 
$$EAT = (1-p_{page\_fault}) \times T_{memory\_access} + p(T_{overhead} + T_{swap\_out}+T_{swap\_in})$$       
- (1-p) is non-page fault access probability

If for example the average page fault service time is 8 mili-seconds and memory access time is 200 nano-seconds. If one access of 1,00 causes a page fault then p -> 0.001. In this example, EAT = 8.2 ms which is a 40 times slower access on average! 

# Copy-on-write (COW)
process creation using the fork() system call. It allows the parent and child processes to initially share the same pages 
- marks the shared pages as copy-on-write pages
- if either process modifies a shared page, a copy of the shared page marked as copy-on-write is created 
- pages containing executable code are often shared b/w the parent and child processes without being marked COW 

this offers the advantage of only needing to copy specific pages for parent and child processes 

# vfork() (virtual memory fork)
- variation of the fork() system call
- operates differently from fork() copy-on-write 
-  **suspension** the parent process and uses the address space of the parent process 
- this allows us to load a new program with exec() without copying all the data from the parent processes as its done with fork() 
	- delayed memory allocation without overhead of copying 
	- intended to be used when the child process calls exec() immediately after creation -> very efficient 

# Page Replacement 
a method used in virtual memory systems to manage paging in and paging out of pages from main memory into secondary storage he page after being loaded 
- used to modify the **dirty bit** to reduce overhead of paging out - only modified pages are written to the disk 
	- a dirty bit to indicate the modification in the page after being loaded into the cache memory 
the process of page replacement completes the separation between logical and physical memory 

### Process for Page Replacement 
1. find the location of the desired page on the disk
2. find a free frame 
	1. if theres a free frame use it
	2. otherwise use a page replacement algorithm to select a victim frame 
3. bring the desired page into the newly freed frame; update the page and frame tables
4. continue the process by restarting the instruction that caused the trap 

### Optimal Page Replacement 
optimal is defined at the lowest page-fault rate 
- replace the page that will not be used for the longest period of time

![[Screen Shot 2024-03-20 at 10.24.37 AM.png]]

choose the page for replacement that will not be used **for the longest time**


### Least Recently Used (LRU)
replace pages that have not been used in the longest amount of time (this lets us use past knowledge)

![[Screen Shot 2024-03-20 at 10.28.45 AM.png]]

# Allocation for Page Replacement 
depends on the scheme of the operating system. Say we have the following case 
- 128 frames
- 35 os frames
- 93 user process frames 
- under pure demand paging, all 93 frames would initially be on the free-frame list 
a user processes would generate a sequence of page faults until the all free frames would be obtained 

### Equal Allocation
divide the total number of frames by the number of processes to get a uniform number of frames per process
- i.e. 100 frames, 5 processes => 20 frames/process 

### Proportional Allocation 
allocate according to the size of the processes

![[Screen Shot 2024-03-20 at 10.32.54 AM.png]]

### Priority Allocation 
uses a proportional allocation scheme that uses priority rather than size 

### Global replcaement
processes selects a replacement frame from the set of all frames
- processes can steak frames for each other
- greater throughput with variable execution time 

### Local Replacement
each process selects from only its own set of allocated frames
- more consistent per-process performance
- possibly underutilized memory 


# Thrashing
a process is busy with swapping pages in and out. This occurs when the total memory demand is greater than the physical memory size. 

if a processes does not have "enough" pages, the page-fault rate is very high
- page fault to get to the page itself
- leads to...
	- low cpu utilization
	- another processes can be added to the system to increase the degree of multiprogramming -> makes the problem worse 
![[Screen Shot 2024-03-20 at 10.36.41 AM.png]]

there is a threshold where the physical frame size allocated to processes will incur high rates of swapping and time will be spent swapping instead of actually computing with the cpu.

# Locality
a set of pages that are actively used together. As a process executes, it moves from locality to locality. 
- a program generally consists of several localities which may overlap 
![[Screen Shot 2024-03-20 at 10.40.53 AM.png]]

# Working-Set Model
a dynamic page replacement algorithm that allocates frames to a particular process assuming that the nearest future of pages will be used is a close approximation of recent page use 
- algorithm based on locality
-  If a page is in active use, it will be in the working set.  
- If it is no longer being used, it will drop from the working set  
-  A theoretical concept for understanding process behavior  

![[Screen Shot 2024-03-20 at 10.44.12 AM.png]]

the value D is the summation over all working sets. If this sum of frames is greater than total number of available frames then a process may experience shortages of frames which means you should try suspending or swapping out a process. 


### Working Set Procedure
1. the os monitors the working set of each process and allocates to that working set enough frames to provide it with its working set size as long as there are enough extra frames 
2. if D>m, the os selects a process to suspend and one to swap in for it

this scheme prevents thrashing and optimizes cpu utilization. It is how ever difficult to keep track of the working set with low complexity 

![[Screen Shot 2024-03-22 at 10.17.19 AM.png]]
- at $t_1$ our $WSS$ is 5
- at $t_2$ our $WSS$ is 2 

### Relationship Between Working Set and Page-Fault Rate
there is a direct relationship between these two attributes. The working set changes over time and the its not a constant value.
![[Screen Shot 2024-03-22 at 10.24.41 AM.png]]

# Kernel Memory
the memory partition of modern operating system. This memory is often allocated from a free-memory pool with some parts of it requiring contiguous space
- kernel mode and user mode
- fundamental aspect of protecting the stability, security, and integrity of the operating system and the applications  running on it
- kernel memory is treated differently than user memory 

### Buddy Allocation System
an algorithm in which a larger memory block is divided into small parts to satisfy the memory request 
- hierarchical
- memory blocks of varying size on the power of 2 
- often used for kernel memory management (e.x. in linux) 
- allocates memory from a **fixed-size segment that consists of physically contiguous pages**

each request is rounded up to the next highest power of 2. When smaller allocation size is needed than available, the current chunk is split into two buddies of the next lower power of 2. There is a disadvantage of **internal fragmentation**. Theres a tradeoff between external and internal fragmentation by offering finer granularity in memory allocation. 

![[Screen Shot 2024-03-22 at 10.33.55 AM.png]]

### Localities in Cache Memory 
- temporal locality
	- if some variables are referenced by a program, it is highly likely that the same might be referenced again later in time
- spatial locality
	- it is highly likely that any consecutive storage in memory might be referenced sooner 

![[Screen Shot 2024-03-22 at 10.36.50 AM.png]]

# Tradeoff between internal and external fragmentation
these algorithms try to balance between these 2 forces. If we allocate based on the requesting processes, this might incur external fragmentation. If we allocate based on the OS requirements and other processes, this might incur internal fragmentation 

# Slabs 
the primary unit of currency in the slab allocator. Each slab contains some number of objects with the same type. Each slab has 3 states: 
- full 
- partial
- empty

when some part of the kernel requests a new object, the request is satisfied from a partial slab, an empty slab, or a newly created slab
![[Screen Shot 2024-03-22 at 10.46.30 AM.png]]
### Slab Allocator 
an object-caching kernel memory allocator. The basic idea is to have caches of commonly used objects to be kept in an initialized state available for use by the kernel
- maintaining a pool of pre-allocated objects 
- pooling mechanism to reduce dynamic memory allocation overhead 
![[Screen Shot 2024-03-22 at 10.40.29 AM.png]]

when an object is requested, it first checks if there are any available objects in the cache that already exist and match the requested size. If it does exist, it retrieves it, updates it if necessary and then returns the address of the cached object.
- storing entire slabs or segments of slabs within cache lines (a block of cache memory) -> promotes efficiency 
- the main goal is to improve efficiency 
**we would like to have as contiguous as possible of allocation of objects over slabs** 