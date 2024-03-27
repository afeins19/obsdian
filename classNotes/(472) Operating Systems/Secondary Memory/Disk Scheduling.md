# Disk Partitons 
recall that cylinders are stacks of cylindrical sections of the drive disks with some radius r.

# First Come First Served (FCFS)
 The simplest algorithm involves just moving the r/w head to the next needed read section 

# Shortest Seek Time First (SSTF)
selects the request with the **minimum seek time** from the current head position
- similar to shortest job first scheduling 
- may cause starvation of some requests 

# SCAN Algorithm 
the disk arm starts at one end of the disk and moves toward the other end, servicing requests until it gets to the other end of the disk. The movement is then reversed and servicing continues 
- sometimes called the elevator algorithm 
- This ensures that any potential requests requests located at the end can be efficiently serviced 

# Circular SCAN (C-SCAN)
head moves from one end of the disk to the other servicing requests as it goes. However when the head reaches the end of the disk it immediately jumps back to the start of the disk. 
- treats t he cylinders as a circular list that wraps around from the last cylinder to the first one 

C-SCAN jumps to the initial starting point with a very small latency 

# General Notes on Disk Scheduling
- sstf is common and has a natural appeal
- scan and c-scan is useful for systems that place a heavy load on the disk
	- less starvation
	- efficiently serviced with minimal arm movement 
- performance depends on the number and types of requests 
- requests for disk service can be influenced by the file-allocation method and metadata layout 

# Logical Block
the base unit for data transfer or the atomic unit of storage handling. Physically on the disk, a segment is some $\Delta angle$ at some radius on the disk (a section of disk at radius r).   

### Logical cluster
- basic allocation unit for a file
- multiples of logical allocation units 
- hard disk space is assigned as multiple unit of logical clusters for each file
- simplifies the file management and reduces the overhead from large memory addresses 
- a file only 1 byte long -> 1 cluster allocated 
- a file only 1 bytes bigger than the size of a cluster -> 2 clusters allocated 

# File Allocation Table (FAT) 
data structure that contains information about the layout and physical location of files on the disk 
- files are stored as a linked list of blocks in the table where each element in the list contains the location of each block 
- a file may have any number of entries
- entries are made in the fat table to keep track of the location of files on the drive 
- used in combination with directory entry table 
	- an entry consists of filename and starting blocks or clusters 

# Disk Data Structures 


### Partitions 
the division of the disk into one or more groups of cylinders, each treated as a logical disk 
- partition -> a logical division of the hard disk 

### Volumes 
a single accesable storage block 

# Disk Management 
to increase efficiency, most files systems group blocks into clusters 
- reduced metadata overhead
- encourages data contiguity -> reduced access time 
- reduced fragmentation thanks to continuous blocks 
- raw disk acess for apps that want to do their own block management -> keeps the os out of the way (e.g. databases)

### Sector Sparing
used to handle bad bblocks
- executed by the disk controller
- maintains a list of the bad blocks and keeps updating the list 
- logically replaces the bad block with a spare sector when required 