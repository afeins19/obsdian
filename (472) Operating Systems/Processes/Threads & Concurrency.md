most applications are multithreaded. Multiple tasks with the application can be implemented by separate threads. process creation is weight while thread creation is weight so multithreading increase efficiency. Threads might handle:
- update display
- fetch data 
- spell checking 
- answering a network request 

### Benefits of threads 
- responsiveness - allows continued execution if part of the process is blocked
- resource sharing - threads share resources of processes easier than shared memory or message passing 
# Multithreaded server architecture
- uses multiple threads within a server to handle concurrent client requests 
- assigning each connection to a separate thread from reusing threads from thread a pool 

![[Screen Shot 2024-01-31 at 10.44.17 AM.png]]

