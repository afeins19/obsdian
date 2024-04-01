### Clusters 
the most atomic quantization of files - all files are made of multiples of a single cluster 

a file is the basic logical storage unit for the operating system 
- a uniform logical view of stored information
- abstract data type 
- a named collection of related information that is recorded on secondary storage 
- the allocation of logical secondary storage from a users perspective
	- data cannot be written to secondary storage unless it is within a file (all data must reside within some file)
- a file may be 
	- a program 
	- a device that you use (especially in linux

### Unix Approach to Files
"everything is a file in linux"
- devices are represented as files in the file system 
- accessible using standard file i/o operations and system calls 
- consistent and unified way of interacting with various devices 
- device files are abstractions of standard devices 

**psuedo devices** - a software babsed constract in an OS that mimics the behavior of physical hardware devices (/dev/random)
- directory is a file with information on how to find other files 

### Device Filles 
an interface to a device driver that appears in a file system as if it were an ordinary file
- a form of abstraction that hides the intricate details of hardware devices from user-space applications 
- entry point or interface that allows the user space applications to talk to the kernel and request operations from the hardware 

### File Descriptor 
a non-negative integer to represent the file
- 0,1,2 corresponds to STDIN, STDOUT, and STDERR respectively 
- process control block contains a table, the file descriptor table that gives the mapping between the descriptor the processes use to refer to a file connection
- descriptors can point to open files, sockets, pipes, or other types of I/o 
- **maintained at the process level** 

# File System 
a method or structure for organizing and storing data on storage devices
- allows users and programs to interact with files and directories in a consistent and efficient manner 
- defines how files are named, stored, and retrieved from a storage device 

### File Management Systems
- **Inode table** - containing metadata about each file in the file system such as file permissions, ownership, and pointers to data blocks where the files contents are stored (managing underlying structure of files) each system only has **one inode table**
- **File Allocation Table (FAT)** - maintaining a map of which clusters (or blocks) on the disk are allocated to each file and which are free for use -> location tracking (manages open files from the perspective of processes)
- **Directory Table** - organizing the directory structure of the file system, storying information about directory entries such as file names and pointers to their corresponding inodes 

# File Attributes 
- name - the only information kept in human readable form 
- identifier - unique tag to identify the file within the system
- type - needed for systems that support multiple types 
- size - current file size
- protection - security controls over access/modification privileges 
- time, date, user identification - protection, security, and monitoring 
- information about files are kept in the directory structure

note that the size of the file itself and the size on the disk varries due to the os storing other metadata as well as allocating certain amounts of space extra. 

# file pointer (also called FILE)
the standard library internal data structure representing a file on the disk 
- interacts with the os and the file system to perform the requested operations 
- creating a n object used to access and manipulate data within the file 

# File as a Data Structure 
a file may be considered as a data structure with some essential operations 
- create 
- write - at write pointer location
- read - at read pointer location
- reposition within file - seek 
- delete 
- truncate 
- Open($F_i$) - search the directory for entry $F_i$
- Close($F_i$) - move the content of $F_i$ (currently in memory) to the directory structure on the disk

### Open File Table 
- tracks open files 
- holds file pointer: pointer to the last r/w location per process that has the file open
- file-open count - counts the number of times a file is open 
	- how many times the current file has been opened but not closed by some process 
	- if 0, file may be removed from the table 
- Disk location of the file 
- access rights 
- per-process open file table and system-wide open file tables exist 

# Open File Locking 
provided by some operating systems and file systems
- similar to r/w locks
- shared lock is similar to reader lock - several processes can acquire concurrently 
- exclusive lock similar to writer lock 
### Mandatory  lock 
access to a file depends on the locks held and requested (lock is enforced)

### Advisory lock 
processes can choose whether to respect the lock or not 


# Fork() call on process with open files 
the child processs inherits a copy o the parent process's open file descriptors and their associated information
- the child process also has access to the same open files as the parent process at the time of forking 
- same file descriptors 
- same file position
- same status flag 

there are **two different locking mechanisms**:
- record locks associated with a process
- **file descriptor locks associated with a file** 

# Record Locks 
locks associated with the process
- fcntl commands to support record locking 
- released when the file is closed by a process or a process exits 
- **not inherited by the child process when fork() is used**
- specified when making a lock by using `flock` 
- **locks are specific to each process** 
- **the parent process can maintain exclusive access to the file** until it releases the file lock, ensuring data integrity and preventing concurrent modifications by child processes 

# File Descriptor Locks 
associated with an open file description rather than a process
- open file description is an instance of an open file and an open file description which is the numeric value that refers to the open file description 
- inherited by child processes across fork along with the file descriptor 
	- child process can access the file
