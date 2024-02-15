multiple processes accessing and writing to variables is something that must be managed. 

- Background  
-  The Critical-Section Problem  
- Peterson’s Solution  
- Mutex Locks  
-  Semaphores  
-  Synchronization Hardware  
- Bounded buffer problem  
- Synchronization Examples  

**Example:** video compression algorithms represent  each video frame as an array of 8-pixel by 8-pixel macroblocks. Each macroblock is individually compressed. Performing the macroblock compressions concurrently with a mullti core processor is way to do this quickly


**problem:**  processes can execute concurrently which means that 
- they may be interrupted at any time, including partially during completing execution
- concurrent access to shared data may result in data inconsistency
- maintaining data consistency requires mechanisms to ensure the orderly execution of cooperating processes 

# Race conditions 
two processes trying to perform two conflicting actions simultaneously and the outcome is not predictable. For example, performing the same actions over the same resources. 