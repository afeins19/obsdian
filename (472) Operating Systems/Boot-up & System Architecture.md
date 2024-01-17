# Boot-up Process 
1. startup: switching power on to supply electricity to main components like the basic input/output system (BIOS)
	- bios manages data flow from the os and attached devices 
2. Power on self Test (POST): an initial test performed by the bios
	- checks i/o, memory, disk drives, among others 
3. OS Startup 
	- loading OS onto main memory 
4. System Configuration
	- loading drivers onto main memory 
5. Basic program boot up 
	- first programs to run on your computer (antivirus, volume control, etc.)
6. Authentication: password authentication for users if necessary 

# Device Controllers 
	 an abstraction of a hardware device, it acts as an interface between the cpu and the hardware (although they may sometimes may be built-in to the cpu)

 - Each hardware device usually has a set of registers to important information such as state
 - internal device controllers have a local buffer (a small temporary storage area used to hold data while its being moved or processed) 
- CPU moves data from/to main memory to/from local buffers 
- Device controllers can inform the cpu that it has finished some process by way of an **Interrupt**

![[Screen Shot 2024-01-10 at 10.36.14 AM.png]]

# What is I/O

**input:** the process of recieving data from external devices into the computers memory or processing unit (e.g. keyboard input)

**output:** the process of sending data from the computers memory or internal storage to some external connections 


# Interrupts 
a hardware or software signal that demands **immediate attention by an OS**
- hardware events
- errors
- requests for services

![[Screen Shot 2024-01-10 at 10.39.10 AM.png]]

# Storage 
	storage systems are organized into a heirarchy 
	- speed
	- cost
	- volatility
### Main Memory (Primary Storage)
- random access: access to any location without sequential scan 
- typically volatile 
### Secondary Storage 
- extension of main memory that provides large, non-volatile storage 
- things such as HDDs, SSDs, optical disks, usb, etc. 
### Hard Disks 
	note that the CPU will not directly interact with the Hard disk but will rather interface with the disk controller 
- divided into tracks which are further divided into sectors 
- disk controller determines the logical interaction between the device and the computer
### SSDs
- faster and non-volatile 


# Caching 
	copying information into a faster storage system; main memory can be viewed as a cahce for secondary storage. The system checks the next fastest layer of memory for data and if it is absent goes to the next fastest and so on.
### Levels of Caching 

![[Screen Shot 2024-01-10 at 10.49.29 AM.png]]
- as we move down, the storage mediums are slow, but cheap and have large capacities
- moving up, we trade off high cost and low capacity, for high speed 

# Von Neumann Architecture
![[Screen Shot 2024-01-10 at 10.55.22 AM.png]]

# Multi Core CPU

- each core of a multi-core processor has a **dedicated L1 cache** and is usually not shared between the cores
-  there are also L2 & L3 caches that are shared between processors 

![[Screen Shot 2024-01-10 at 10.57.43 AM.png]]
# Clustered Systems
	like multiprocessors systems, but multiple systems working together
- usually sharing storage via a storage-area-network (SAN)
- provides high-availability (HA) service which survives failure 
	- asymmetric clustering has one machine in hot-standby mode
	- symmetric clustering has multiple nodes running applications, monitoring each other 
- High-performance computing (HPC)
	- applications must be written to use parallelization 
	- E.g. Hadoop 