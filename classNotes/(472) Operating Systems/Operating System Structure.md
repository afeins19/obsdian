# Multiprogramming (Batch System)
- organizes job (code and data) such that the CPU always has one to execute
- subset of total jobs in system is kept in memory
- one job selected and run via job scheduling 
- when it has to wait (for i/o for example), the OS switches to another job 

### Memory Layout  of Multiprogram System 
![[Screen Shot 2024-01-12 at 10.16.12 AM.png]]

# Timesharing (Multitasking)
	the CPU switches jobs so frequently that users can interact with each job while its running, creating an interactive setup for users
- response time should be < 1 second
- each user has at least one program executing in memory -> process
- if several jobs are ready to run at the same time -> scheduling 
- if processes don't fit in memory, swapping moves them in and out to run them 

# Interrupt Driven (Hardware & Software)
- Hardware interrupt by one of the devices
- software interrupt (exception or trap)
	- software error (division by 0)
	- request for some Operating System Service
	- other process problems include infinite loop, process modifying each other or modifying the operating system itself 

# Dual-mode (System Calls)
	allows the OS to protect itself and other system components. We can't allow programs to conflict with other programs, such as stealing memory. 

- **User Mode & Kernel Mode**
	- a hardware supported feature provided by the computer's CPU 
	- **Mode bit**: a bit that indicates the current mode of execution 
		- stored in the program status word (PSW) register of the CPU
		- mode bit = 0 -> kernel mode -> privileged execution 
		- mode bit = 1 -> user mode -> restricted access to system resource 
- A system call 
	- a request from some program to an operating systems kernel
	- acts as a **link between the operating system and a process,** allowing user-level programs to request operating system services 

### Transitioning from User to Kernel Mode 
	the transition from user mode to kernel mode during a system call is usually made promptly as long as the necessary resources are available 

- Timer is set to interrupt the computer after some time period  
- Keep a counter that is decremented by the physical clock.  
- Operating system set the counter (privileged instruction)  
-  When counter zero generate an interrupt so that it can  
execute system call in kernel mode


# Processes 
	a program in execution. It is an active entity.
- resources required to accomplish its task by the process 
	- cpu/memory, i/o, files
	- initialization data 

- has a program counter for each **thread** 
	- specifying location of next instruction to execute 
	- process executes instructions sequentially, one at a time, until completion

- **thread**
	- a sequential flow of tasks within a process 
	- smallest unit of programmed instructions that can be managed independently by a scheduler 
	- multi-threaded process has one program counter per thread 
	- **concurrency** is facilitated by multiplexing the cpus among the processes/threads 

# Process Management Activities 
	operations that facilitate the operation of multiple processes

- **creating** and deleting both user and system processes
- **suspending** and resuming processes 
- **synchronizing** processes 
- providing **communication** between processes 
- providing mechanisms for **deadlock handling**
	- the handling of blocked processes due to a resource conflict between some processes 
	- this occurs due to 2 processes requiring each others resources. This might result in an indefinite wait 

# Memory Management 
- to execute a program, all (or part) of the instructions must be in memory 
- all (or part) of the data that is needed by the program must be in memory 
- memory management determines what is in memory and when 
	- optimizing cpu utilization and computer response to users 
### Memory Management Activities
- **keeping track** of which parts of memory are currently being used and by whom 
- **deciding** which process (or parts thereof) and data to move into and out of memory 
- **allocating** and deallocating memory space as needed 

# Storage Management 
	the operating system provides a uniform, logical view of information storage 
- abstracts physical properties to a logical storage unit - **file** 
	- properties such as access speed, capacity, data-transfer rate, access method (sequential or random) 
### File System Management 
- files are usually organized into directories 
- **access control** on most systems to determine **who can access what**

### OS Storage Activities 
- **Creating** files & directories 
- **Deleting** files & directories 
- **Mapping files** onto secondary storage
- **Back Up** files onto stable (non-volatile) storage media 

### Mass Storage Management 
	usually disks used to share data that does not fit in main memory or data that must be kept for a "long" period of time. The entire speed of computer operation hinges on disk subsystem and its algorithms 
### OS Mass Storage Activities
- Free-space management 
- storage allocation
- disk scheduling 

### Performance of Various Levels of Storage 
![[Screen Shot 2024-01-12 at 10.48.57 AM.png]]
- *note*: registers and cache (managed by CPU) are both coordinated from the OS 

# I/O Subsystem
	controlls the communication between the central processor and all peripheral devices (hardware such as disk units, printers, etc).
- one purpose of the os is to hide peculiarities of hardware devices from the user that are specific to that piece of hardware 
### I/O Interface
![[Screen Shot 2024-01-12 at 10.54.00 AM.png]]

# Protection and Security 

### Protection 
	 any mechanism for controlling access of resources by users or processes 
### Security
	defends the system against internal and external attacks 
systems generally first distinguish among users, to determine who can do what 
- user identities (such as user IDs, security IDs) including name and associated number (one per user)
##### Some Possible Threats 
- DOS attacks
- Worms
- Viruses 
- Identity Theft 

# Operating System Services 
### File System manipulation 
	programs need to read and write files and directories, create and delete them, search them, list file information, and manage permissions. 
### Communication
	processes may exchange information on the same computer or between computers on a network. The OS facilitates this. 
### Error Detection
	the OS needs to be constantly as aware as possible about possible errors
- may occur in the cpu and memory hardware, i/o devices, or user programs
- for each type of error, os should take an appropriate action to ensure correct and consistent computing
- debugging facilities can greatly enhance the user's and programmer's abilities to efficiently use the system
### Resource allocation
	when multiple users or multiple jobs are running concurrently, resrouces must be allocated to each of them 
- many types of resources - cpu cycles, memory etc.
### Accounting 
	keeps track of which users use how much and what computer resources 
### Protection 
	protection involves ensuring that all access to system resources is controlled 
### Security
	protects the system from outsiders, requires user authentication, extends to defending external i/o devices from invalid access attempts 

# Interfaces 

## Command Line Interface (CLI)
- getting the user to input a command that will directly be executed 
- it reads commands from the user or from a file of commands and executes them. Usually turns commands into one or more system calls 

### Shell 
	a command interpreter given through the terminal. It is both an interpreter and a programming language 
- provides the user with an interface to the kernel
- named a shell because it is the outermost layer around the operating system
- assigned by os after logging through terminal (using shell over the terminal)
	- sometimes, terminal and shell are used interchangeably 
	- terminal is a text-based interface
	- shell is a command-line interpreter 

## Graphical User Interface (GUI)
	user-friendly desktop metaphor interface which allows users to interact using a mouse, keyboard, and a monitor. icons represent files, programs, and actions. various mouse buttons over objects in the interface cause various actions. 

### Touch Screen
	mouse is not possible to be used or desired. Actions and selection based on gestures. Virtual keyboard is used too. 

## Design Trade-offs 
- simplicity vs. feature-richness
- consistency vs. customization
	- degree of customization 
- visual appeal vs. performance
- accessibility vs. simplicity 
	- accessibility features like screen readers and voice commands 
- discoverability vs. efficiency
	- making features easily discoverable to newcomers 
- security vs. convenience 


