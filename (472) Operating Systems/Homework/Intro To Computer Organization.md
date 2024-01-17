 ,1234e# The User's Perspective
	how do different kinds of users interact with computers?
- personal computer
	- screen interface
	- keyboard
- smartphone
	- similar to pc but features microphone, cameras etc.
- car 
	- steering while position
	- throttle position 
	- display information through gauges/screens 

we interact with computers through some I/O channels, whatever they may be for the given application 

**Hardware:** the physical construction of a computer 
**sofware:** the programs/apps that we run on the computer that define its behavior 

# The Programmers Perspective
- using a computer to develop software, usually with some high level languages
- working with programs (like compilers) that converts programs into machine code 
- usually, programming environments abstract away the fine details of translating your program into a .exe

# The Silicon Perspective 
- computer hardware consists of transistors implemented on silicon 

# Microarchitecture Perspective
- digital blocks implemented on silicon that make up a computer
- executes a series of *low level instructions* 
- the low level instructions come from some program written in a *high level language* 
- the instruction set architecture is the set of all commands that will run on some micro-architecture 

### Some Examples of Microarchitecture
- x86 - supports intel processors 
- Advanced RISC Machine (ARM) - most widely used architecture
- AVR (alf and vergards reduced instruction set) - used by arduino

# Microarchitecture Design ![[Screen Shot 2024-01-14 at 6.34.39 PM.png]]

- processor: active block of the computer thats responsible for following the instructions making up a program
- Memory: location where programs and data are stored
- I/O: any interface with the computer
- Bus: one or more wires that run in parallel and carry data
- Microprocessors (MPUs): supported by several external chips that implement memory, i/o, etc. 
- microcontrollers (MCUs): all functionality contained on a single integrated chip 

### Buses 
	digital connections between functional blocks (abstraction)

- **Serial:** one bit is transmitted at a time. Usually consists of one wire for data and few others for clock and control signals

- **Parallel:** several bits are transmitted simultaneously, usually implemented using several parallel wires (simultaneous sending of bits)

![[Screen Shot 2024-01-14 at 6.39.28 PM.png]]

# Specialized vs Generalized Computing
- micro architecture is the ultimate in generalized computing 
	- actions take by the processor come from instructions stored in memory - a stored program 
	- we change what the processor does by changing the instructions, we don't have to modify any hardware 
- Some digital circuits are designed to only do one job
	- could be a specific chip (wifi chip)
	- FPGAs 
	- ASICs
	- very fast, efficient 
	- not versatile 

- Specialized hardware
	- digital signal processors (DSPs)
	- GPUs (polygon rendering)

# Embedded Design & Firmware 
- embedded system is a computer that is embedded in a larger system that does a very specific job
- Examples: ECU for car, home security system controller 
- Embedded Systems still use a stored program microarchitecture 

### Firmware
	the software that provides very low level control of the hardware 