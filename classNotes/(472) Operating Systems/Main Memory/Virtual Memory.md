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


