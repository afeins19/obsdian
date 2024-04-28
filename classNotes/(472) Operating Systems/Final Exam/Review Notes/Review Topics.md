# Device Driver vs. Controller 

### Device Driver
- device driver is a software component that allows the operating systems and applications to interact with hardware 
- an interface between hardware devices and operating systems 

### Device Controller 
- a physical hardware component (chip) that manages I/O operations between hardware devices and the CPU
- most hardware devices have one (network cards, drivers, usb devices etc.) 
- the actual component that handles cpu instructions 

# ioctl (command)
- a system call that provides a generic interface to send device-specific control commands to device drivers. 
- general purpose command that lets you interact with almost any kind of device
- `int fd`  - the file descriptor that represents an open file which is how the device is abstracted by the operating system
- `unsigned long request` -represents a device specific command or request. Usually defined in the device driver. 
- additional pointers to configuration structs 

# Processes 

### Deadlock 
a state in which the operating system has a circular allocation graph. If two or more processes are waiting for each other to release resources in a way that a cycle of dependencies is formed causing all of the processes to get stuck. 

### Unsafe State 
- doesn't garuntee a deadlock but indicates a condition where its a deadlock is possible, The system is in an unsafe state if there exists a sequence of processes that could request additional resources leading to a scenario where the necessary resources to satisfy these requests can't be allocated without leading to a deadlock. 

### Dependency Graphs 
- nodes can represent processes or resources 
- edges represent relationship between processes and resources 
	- request edge - directed from a process to a resource indicating that the process requests that resource
	- assignment edge - directed from a resource to a process indicating that the resource is currently allocated to the proecss 
- request cycles **do not garuntee** deadlocks but seriously suggest them

# IPC 

### Shared memory 
- the kernel can allocate memory space for some processes that once set up, will not require any help from the kernel to facilitate communication between the processes

# Threading 

### pthread_create()
runs a thread which performs the instructions in a supplied function. 
- note that the system does not wait for the thread to finish before continuing 

### pthread_join() 
instructs the system to wait for the passed in thread to finish executing before continuing 

### Stack 
the stack represents the individually allocated space for each thread and is not shared. This stack contains local variables, function parameters, return addresses , adn the threads call history 

### Heap 
- when multiple threads are spawned from a processes the heap is used as a central location for them to share space for these processes. This is a dynamically allocated space that processes may allocate space and unallocated space from as they wish but might lead to problems like race conditions, synchronization, etc.
- threads can read, write, allocate, modify this space freely. 

## Schemes 

### Many-to-One Model
many user-level threads are mapped to a single kernel thread.
- all thread management is done by the user-level thread library 
- doesn't require support from the kernel for threading 
- since all threads are managed by a single kernel thread, only one can actually be executed ata time even if multiple CPUs are available. 
- if one thread makes a blocking call then all threads will be blocked 

### One-to-One Model 
each user-level thread corresponds to one kernel thread -> each user thread can be managed directly by the kernel 
- allow for most amount of concurrency and takes advantage of multiprocessor systems 
- if a thread performs a blocking operation, it does not affect the ability of other threads to execute 
- requires more overhead from the kernel since each thread is a fully-fledged kernel thread
- creation and management overhead is more time consuming that for user-level threads 

### Many-to-Many Model 
dynamically allocates kernel threads to user threads as required. Allowing for greater flexibility than one-to-one. 
- user threads can be managed independently in the user space and blocking calls can be handled more efficiently  
- more complex to program and manage 
- sophisticated algorithms are required to balance user threads across kernel threads 

# I/O

### Sequence of operations for I/O handling in the OS

system call -> i/o substystem -> device driver -> device controller -> Interrupt generation -> ISR (interrupt service routine) execution -> i/o subsystem -> device driver -> processes 


# Files 

### Inodes 
inode = index node. This is a data structure used to represent a filesystem object which may be a file, directory, or symbolic link. The inode contains the metadata about a filesystem object except for its name and the actual data that it contains 
- file size
- file location on disk 
- file identification 
- file permisions 
- owner 
- file type 

### Inode Table 
maintains a list of inodes that uniquely identify files within its file system.

### File Descriptor 
a file descriptor is a small, non-negative integer that uniquely identifies and open file for the duration of a process. So it's a temporary address for the process to use. it is used by the operating system to reference files or other i.o resources such as pipes or network sockets. 

### File Allocation Table (FAT)
essentially a map of the disk indicating which clusters (or blocks) are used by files and directories. It also tracks which clusters are free and which are reserved and the order of clusters that belong to a file. 

# Memory 

### Physical Blocks 
- sectors: the smallest addressable units of storage on a physical disk
- addressed by their physical location on the disk 
- low level physical addresses of data on the disk 
### Logical Blocks
- an abstraction by the filesystem to manage and reference data storage on the disk -> represents a logical unit of storage as managed by the operating systems filesystem layer 
- used by the filesystem to organize and keep track of where files are stored on the disk each file can be broken down into one or more logical blocks 
- allow for efficient data handling -> logical blocks are larger chunks of space than physical blocks and require less i/o operations than bouncing between smaller physical blocks 
- abstract away the details of physical disk access providing a uniform interface 
### Fragmentation 
- occurs when files are created or deleted. The addressable space they leave open may not be large enough for new files to fit and those files must be written non-sequentially over non contiguous spaces 

### Internal vs External Fragmentation 
- intern fragmentation - when logical block sizes are relatively large. Files are addressed by the OS in multiples of logical blocks (the most atomic unit to the os). This means that if a file doesn't require all the space alloted in the logical block, the remaining space in that block will be unused but reserved for that file. 
- External fragmentation - when contiguous blocks of memory (large sections of logical blocks) do not permit the allocation of a large enough contiguous section for other files
### Memory Management Unit (MMU)
responsible for handling memory and virtual memory management at the hardware level. 
- translates virtual addresses to physical addresses - translates virtual addresses generated by the cpu into physical addresses in RAM.  
- manages access to memory with efficiency and security 
- uses the Translation Lookaside Buffer (TLB) - this speeds up the translation process. The MMU uses a cache called the TLB which stores recent mappings of virtual addresses to physical addresses so it just looks up the ones that are needed. 
- the MMU handles page swapping and virtual memory - The MMU is responsible for managing the swap-space between secondary storage and ram. This lets us run programs that require more space than the RAM allows for! 
-  Page Fault Handling - when a process tries to access a page thats not in memory, the MMU raises a page fault interrupt, which tells the OS to load the required page from the disk into RAM

### Virtual Memory 
an abstraction that allows data to appear to a processes sequentially even though it may be scattered in pieces across ram. 