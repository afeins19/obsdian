# What is a process?
**What is a process**: a process is some program that's currently in execution. The execution must progress in sequential fashion (processes are sometimes called jobs)
# Components of processes
this data is stored inside the process control block (PCB) which each process contains. 
- **PID (process identifier)**: each process is assigned a unique identifier. This is how the os tracks the process
- **Program counter**: holds the address of the instruction to be executed next 
- **Stack**: temporary data  like function parameters, return addresses and local variables
- **Data Section**: global variables 
- **Heap**: dynamically allocated memory during run-time 

# Process States 
a process may exist in the following states 
- new - the process has just been created
- running - process instructions are being executed 
- waiting - for some other event to occur or for another process to finish
- ready - the process is waiting to be assigned a *processor*
- terminated - the process has finished executing 

# Threads 
the smallest discrete computation unit to the OS. A process can be divided into multiple threads 
