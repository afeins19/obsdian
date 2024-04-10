# ioctll() system call 
a system call for manipulating the underlying device parameters of special files. Recall that in Linux devices are essentially treated as files. This system call provides a way to interact with devices and their drivers beyond just simple read and write operations. 

arguments: 
- fd: an open file descriptor
- a device dependent request code
- \*argp - untyped memory pointer

**ex**: loctl(fd, TOICGWINSZ, &ws)

- FIONREAD to determine the number of bytes available for reading on a file descriptor 
- VIDIO_QUERYCAP (video capture query capabilities) to retrieve information about the devices capabilities such as supported video formats, frame rate, etc. 

### Additional Functionality of ioctl()
- clock and timers for IO - a continuous and consistent reference of the passage of time
- provides current, elapsed time, and regular timer 
- default capture frequency is 1/60 second 

# Schemes for a process to interact with I/O Operations

### Asynchronous I/O 
- i/o call returns immediately without waiting for the operation to complete
- the i/o subsystem signals process when i/o completes -> interrupt or call back
- difference between nonblocking and asynchronous i/o
	- a nonblocking read() returns immediately with whatever data is available 

# Kernel I/O Subsystem
a fundamental component of modern OSs which is responsible for managing I/O 

- Buffering - used to store data in memory while transferring between devices
	- used to cope with device speed mismatch
	- copes with device transfer size mismatch
		- the size of data that a device can transfer in a single operation (such as a read/write) might not align with the OS's 
	- used to maintain "copy semantics"
		- after x is copied into y, they are equivalent and independent 
		- the version of data in the buffer is guaranteed to be the version of data at the system call 

- double buffering - two copies of the data
	- using two buffers to speed up a computer that can overlap I/O with processing 
		- e.x. one for rendering and another for displaying an image 
	- copy onw write can be used for efficiency in some cases 
### Scheduling 
the process of managing and prioritizing i/o operations 
- different schemes like devices queues, fairness algorithms, quality of service algorithms 

# I/O Protections from users
user level processes may accidentally or purposefully attempt to disrupt normal io operations via illegal io instructions

- we can solve this by defining all io instructions to be **priviledged**
	- users cannot directly issue io commands
	- user level processes send requests to the kernel, but kernel decides the time and execution of every io command 

# Kernel Data Structures 
- keeps state info for i/o components, inculding open file tables, network connections, character device states 
- many complex data structures to track buffers, memory allocation and dirty blocks (a block of data that has been modified in the cache)
- some object-oriented methods use message passing to implement i/o
	- leverages principles of object oriented programming to model and manage the complexities of i.o operations 