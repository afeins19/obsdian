These notes discuss the creation, management, and deletion of processes.

# Fundamental Process Operations 
- Creation 
- Termination
- communication 

# Process Creation 
parent processes create child processes, which in turn are the parent processes of child processes started by them. This forms a tree  
![[Screen Shot 2024-01-27 at 1.33.06 PM.png]]
- a child process is created as a copy of its parent process
	- example: execution of text editor in a shell -> the child process of the shell 
- generally, process is given a **PID (Process Identified and Managed)**** 

### Resource Sharing between Parent and Child Processes 
the sharing of resources between parent and child processes are **context dependent** 
- parent and children may share **all resources**
- children may share a **subset of parents resources**
- parent and child might not share **any resources** 

### Execution of Parent and Child Processes
again, the execution order of a parent and its child processes is also context dependent
- parent and children may execute **concurrently** 
- parents **may wait** until child processes terminate 

### Duplication 
there are two main ways in which the address space of a child process can be managed. 

##### Complete duplication 
- duplicating the entire processes even the program counter (**note that this is not copy the code itself**)
- the only difference in this case is between the child and parent process is their PIDs (child is given a unique PID)
- after making a copy, the PID of child process is returned in the parent, and **0 is returned in the child** -> that is how we distinguish between parent and child 

### Address Space Management 
there are 2 main ways in which the address space of a child process can be managed 

##### Copy on write 
the *c* shares *p*'s memory initially, new memory pages are allocated and marked as copy-on-write but are not written to initially. Any change which will be made by one process is **written in another memory address** 
- any process which makes changes will copy the memory to the allocated new address and make changes on that copy 
![[Screen Shot 2024-01-27 at 2.03.56 PM.png]]

# Fork() (system call)
the fork() is the name of the system call for creating a new process in linux. 
- creates a new child process
- the child processes executes the next instruction following the fork() system call

### Resource Sharing with Fork()
the child process uses the 
- same program counter (PC) 
- same CPU registers
- same open files which are used in the parent process 

### Return Values 
Fork() takes **no parameters** and returns an integer value 
- **negative value** - indicates child process creation was unsuccessful 
- **Zero** - return is made to the newly created child process
- **Positive** - return is made to the **parent or caller** -> PID of the child process  

### Fork() on a parent process 
when a **parent** process is forked, Fork() returns...
- the PID of the newly created child process 
- a positively valued integer greater than 0, unique to each process 

### Fork() on a child process 
when a **child** process is forked, Fork() returns...
- a value of 0 which is how we may identify child processes (only child process have a 0 value)

### getpid()
use this function to get a processes **own PID**

### getppid()
use this function to get the **parent process's PID**

# exec() (system call)
the exec() call is used to replace a process's memory space with a new program 
- it keeps the same PID as the process calling exec()
- loading a program is an invocation of exec() 
- it makes changes to the necessary attributes in memory 
- exec() executes the program 
a combination of fork() and exec() are often used when a process needs to execute a different program 

![[Screen Shot 2024-01-27 at 2.20.59 PM.png]]


