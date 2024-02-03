Act as a **conduit** allowing two processes to communicate

# Issues with pipes
- unclear whether communication is unidirectional or bidirectional (it can be either one)
- in the case of two-way communication, is it half or full-duplex? (it can be either one)
- must there exists relationship (i.e. parent-child) between the communicating processes? -> not necessarily 


# Ordinary Pipe
cannot be accessed from outside the process that created it. Typically, a parent process creates a pipe and uses it to communicate with a child process that is created. **Ordinary Pipes are unidirectional (one-way) and require a parent child relationship**
- allow communication in the standard producer-consumer style
- producer writes to one end (the write-end of the pipe)
- consumer reads from the other end (the read-end of the pipe)

![[Screen Shot 2024-01-31 at 10.19.55 AM.png]]

# Named Pipes 
more powerful than ordinary pipes. **Communication is bidirectional** 
- no parent-child relationship is necessary between the communicating processes
- several processes can use the named pipe 
	- several writers
	- several readers
	- persists after communication process has finished 
- supported on both UNIX and Windows systems 

# Pipes in Unix
```bash 
>> <command 1> | <command 2>
```
- pipes the output of *command 1* to *command 2* 

# Sockets 
provide a means for communication between processes over a network. Sockets allow for two-way communication and can be used to connect processes running on different machines. They support various communication protocols, most commonly TCP/IP for network communication. 
- concatenation of **ip and port addresses** allows for precise routing of the messages between sockets 
- communication consists of a pair of sockets
	- all ports bellow 1024 are well known and used for standard services
	- special ip address 127.0.0.1 (loopback) is used to refer to system on which the process is running

![[Screen Shot 2024-01-31 at 10.30.07 AM.png]]

# Remote Procedure (RPC)
abstracts the procedure calls between processes on networked system. 
- use **stubs** as a proxy for the actual procedure
	- a local representation of the remote procedure
- uses ports for service differentiation
- a procedure call is a sequence of statements 

### Stubs 
proxy for the actual procedure 
- a stub for a remote object acts as a clients proxy (local representative) for the remote object -> abstraction of communication details -> developers can focus on the logical aspects of their application 
- the client side stub locates the server and marshalls the parameters (marshaling means packing the data into a transferrable format)
- the server-side stub recieves the message, unpacks the marshaled parameters and performs the procedure on the server
![[Screen Shot 2024-01-31 at 10.35.03 AM.png]]

### Rendezvous Service 
a rendezvous (called a matchmaker) daemon on a fixed rpc port. **also called a match maker daemon**
- acts as a registry or directory service for distributed processes 
- helps process discover each others locations or services 
![[Screen Shot 2024-01-31 at 10.38.25 AM.png]]

