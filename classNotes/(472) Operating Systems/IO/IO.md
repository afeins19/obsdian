# Host - Controller Protocol
1. the host repeatedly reads the busy bit status register until that bit becomes clear (This is called polling)
2. The host sets the write bit in the command register and writes a byte into the **data-out register** 
3. the host sets the command-ready bit in the command register
4. when the controller notices that the command-ready bit is set, it sets the busy bit
5. the controller reads the command registers and sees the write command. It reads he data-out register to get the byte and does the I/O to the device
6. the controller clears the command ready bit in the command register, clears the error bit in the status register to indicate that I/O was successful and clears the busy bit to indicate that the job was done 
### Polling 
- host repeatedly reads the busy bit 
- fast if device is fast but inefficient if the device is slow - wasting cpu time to poll the device
### Interrupt 
a cpu has a direct line called an interrupt-request line with the I/O controller. When a device does something, the I/O controller tells the CPU through this line. This line is checked by the processor after every instruction. The sequence of an interrupt is:
1. stopping the current operation and saving the state
2. jumping to the ISR (interactive service routine)
3. performing the necessary operation 

# Programmable Interrupt Controller (PIC)
this device tells the cpu that an interrupt with a trigger. Importantly, it also specifies the particular device making that request. If there is an error, the PIC will send a vector number to the cpu informing it of the nature of the error. 
- maskable interrupt: an interrupt that can be disabled or ignored by the instructions of the cpu (essentially a low priority interrupt)


### Interrupt Chaining
a mechanism to manage multiple interrupt requests from different devices 

### Exception Messages through Interrupt lines 
interrupt line can also be used for exceptions 
- terminate processes, crash system due to hardware error
- interrupt for page fault 
	- interrupt by MMU (MMU was a separate hardware component in the old days)
	- the signal for the page fault can be considered as a trap in a modern computer 

# Direct Memory Access (DMA) 
- a technique for transferring data within main memory and external devices **without passing it through the cpu** 
- a way to improve processor activity and i/o transfer rate by taking over the job of transferring data from the processor 
- more efficient when a large volume of data has to be transfered
	- total overhead associated with configuring DMA transfers might be minimal for large pieces of data that are transfered continuously  

### DMA Controllers 
- HW to enable data transfer between two devices without involving the CPU 
- ex. copying data from HDD to a USB stick 

### Basic Operation of DMA
1. the processor issues a command to the dma module by sending some dta
	- r/w command 
	- number of words 
	- starting location in memory
	- address of the I/O device in memory 
2. after the information is sent, the processor continues with its work
3. the DMA module then handles the entire transfer of the block of data directly to or from memory without going through the processor 
4. when the transfer is done, the dma sends an interrupt 

# Application I/O Interface
![[Screen Shot 2024-04-05 at 10.49.46 AM.png]]

- set of techniques and interfaces for an operating system that allows I/O devices to be treated in a standard way
- the interface that allows applications to interact with input and output (I/O devices)
- the I/O system calls encapsulate device behaviors in generic classes
	- device-driver layer hides differences among I/O controlllers from the kernel
	- new devices that speak already-implemented protocols need no extra work
	- each OS has its own I/O subsystem structures and device driver  

this allows fothe abstraction of the detailed differences of various I/O devices
- identifying a few general kinds
- accessing each general kind through a standardized set of functions - an interface
- encapsulating the differences in kernel modules called device drivers 