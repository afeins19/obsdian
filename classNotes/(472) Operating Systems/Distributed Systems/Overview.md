In the modern world, an additional framework is installed on top of an existing OS to support distributed systems. 

# What is a Distributed System? 

# Hadoop 
an apache based architecture for commercially available computers used for the task of data analysis. This architecture distributes work such as visualizing, input gathering, and processing to organize computers into a team that works together

![[Screen Shot 2024-04-19 at 10.15.54 AM.png]]

Formally, a distributed system can be defined as a collection of independent computers that are connected through some communication network that work together to accomplish some goal. Typically, Distributed Systems do not have:
- a shared operating system
- a shared memory 
- a shared clock 

A distributed system consists of loosely coupled processors interconnected by a communications network. processors may be called nodes, computers, machines, or hosts
- site is the location of the processor 
- generally a server has a resource node and a client node 

# Why do we want distributed systems
- scalability
- high availability
- fault tolerance
- reduced latency
- delegated infrastructure and operations 
	- e.g. delegate its storage to AWS 
	- e.g. delegate its customer service system to Salesforce
	- e.g. dlegate its AI chat bot to Microsoft

### Scalability 
this leads to increased performance 
- independent computers are stagnating in their speed increases (or at the rate that moores law states)
- there is a move to heterogeneous computing 
- Horizontal Scaling (distributed load across more systems, scaling out vs. vertical scaling (using more computing power and scaling up the existing systems))

### High availability and Fault Tolerance 
- with large enough systems, something is always breaking
- a service can run even if some systems die 

### Reduced Latency
- cache data close to where it is needed
- e.g. amazon cloud front is a caching service with over 450+ server centers across the US
# Types Of Distributed Operating Systems 
- Network Operating Systems - each node or system can have its own os
- distribute operating systems
	- each node or system must have the same os 
	- loosely coupled systems considered as a single entity 
		- resource sharing over nodes 
# Advantages & Disadvantages of Distributed OS
- Enables fast computation through resource sharing
- easily scalable

disadvantages:
- single point of failure in the main network may disrupt the whole systems 

# Tradeoff between Availability and Reliability
- redundancy and consistency -> availability
- uptime without faults -> reliability 

# Failures 
failures can be classified as one of two kinds: system failures and 


### System Failures
fail-stop
- failed component stops functioning
- detects failed components via timeouts
	- infeasible in asynchronous networks
	- sometimes we just have to guess 

 fail-restart
 - component stops but then restarts
	 - danger: possible stale state - the system was not updated when it was down 
### Network Failures
omission
- failure to send or receive messages
	- this is due to queue overflow in the router, corrupted data, or receive buffer overflow

timing
- messages take longer than expected
	- we may assume a system is dead when it isn't 

partition
- the network breaks into two or more subnetworks that cannot communicate with each other

### Byzantine Failure
a group of generals may be traitors and this supposedly led to the downfall of the byzantine empire. When some component fails in our network it may do so quietly and we need to figure out which one. 

a class of failures in distributed systems where components of the system exhibit arbitrary and potentially malicious behavior such as sending incorrect or contradictory information. 

fail-silent
- no output from a failed component (process or hardware)

##### Solutions 
- practical byzantine fault tolerance (pBFT)
	- a consensus algorithm designed to work efficiently in asynchronous systems with corrective decision making
	- the feature of a distributed network to reach consensus even when some of the nodes fail or respond with incorrect information 