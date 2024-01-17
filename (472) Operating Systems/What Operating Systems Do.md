	note that operating systems are ubiquitous and are not just found in computers! 

# What is an Operating System? 
a program that acts as an intermediary between a user and the computer hardware. The operating system does not allow programs to directly access the hardware. 

after an operating system is loaded  by the boot program, it manages all of the other application programs in a computer. 


	User interface <----> Operating System <----> Hardware (with BIOS)
### OS Goals & Functions  
- execute user programs and make solving user problems easier 
- make the computer system convenient to use
- use the hardware efficiently & manages/divides resources fairly 
- decides between conflicting requests 

# Computer System Structure 
the computer system can be divided into four components 
### Hardware 
- CPU, Memory, I/O 
### Operating System
- Controls and coordinates use of hardware among various applications and users 
### Application programs 
- software entities designed to fulfill specific tasks or provide user functionalities, these programs rely on the OS for resource allocation, management, and interaction with hardware 
### Users 
- people, machines, and other computers 

### Operating System Design
	OS designs on the specifc application (the device and the envirnoment of the device running it

# Major Components of Operating Systems 

### The Kernel
- the core of the operating system that manages system resources like CPU, Memory, and I/O Devices 
- "The single program running at **ALL** times on the computer"

### System Libraries 
- a standard set of functions through which applications can interact with the kernel 

### System Programs
- applications that provide various utilities and functionalities for users such as text editors, command-line shells, and network utilities 

### Kernel Modules 
- a piece of code that can be dynamically loaded into or unloaded from the running kernel without rebooting the system 
- extends the functionality of the kernel such as adding support for new hardware 

# Linux OS

![[Screen Shot 2024-01-10 at 10.21.37 AM.png]]

# Table-based Resource Management 
- **data structures and tables:** ensure effective resource allocation and management 
- **Page Table:** used for virtual memory management in systems that employ paging 
- **Process Control Block (PCB):** Maintains information about a processs including its state, program counter, and register values 
- **Interrupt Descriptor Table (IDT):** Holds interrupt and exception handler addresses in x86 systems 
- **File Allocation Table (FAT):** allocation status in fat file system for removable storage devices
- **Inode Table:** meta data about each file in Unix-like file systems
- **File-Table:** maintains information about open files, such as file descriptors and file status 

