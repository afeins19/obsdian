Security is concerned with unauthorized access, protection is concerned with privileges. 

# The Security Problem 
- system is secure if resources are use and accessed as intended under all circumstances 
	- unachievable 
- intruders attempt to breach security 
- **thread** is potential security violation 
- **attack** is an attempt to breach security 
	- may be accidental or malicious 

## Security Violations 
- breach of **confidentiality** - unauthorized access to data 
- breach of **integrity** - unauthorized modification of data
- breach of **availability** - unauthorized destruction of data 
- **theft of service** - unauthorized use of resources 
- **Denial of Service (DOS)** - prevention of legitimate use 

### Sick Hacks
- **masquerading** (breach authentication) - pretending to be an authorized user to escalate privileges  
- **replay attack** - capturing data such as credentials and replaying it to later gain unauthorized access 
- **man-in-the-middle attack** - interception and potential modification of data flowing between two parties 
	- intercepting communications between two parties  

# Security Types 
- physical - data center, server, terminal
- human - social engineering, phishing 
- operating systems - protection mechanisms, debugging 
- network - intercepted communications, interruptions, DOS 

# Program Threats 
- **Trojan Horse** 
	- seemingly legitimate program with hidden malicious code
	- spyware, popup browser windows, or covert channels 
	- up to 80% of spam is delivered by spyware infected systems 
- **Trap Door** 
	- a secret entry point into a program that allows anyone to gain access to any system 
		- could be included in a compiler 
- **Logic Bomb** - a program that initiates a security incident under certain circumstances 
- **A Bug in  a Program** - could be a bug that causes a major crash in a program
	- stack and buffer overflow
	- when routine returns from a call, it returns to a **hacked address** 
- **unauthorized user or privilege escalation** 

## Stack and Buffer Overflow Attack
- attack through overwriting some buffer areas and replacing return address to execute malicious code 
- languages without garbage collection can be more prone to stack buffer overflows due to manual memory management 

# execvp()
may lead to command injection and path manipulation 
```c
int execvp(const char* command, char* argv[]);
```
- a command as a binary executable file that is a part of the path environment variable 
- `argv` contains the complete command, along with its arguments of **any length**
- any kind of commands may be made -> security risk

# Virus 
a code fragment embedded in a legitimate program 
- self replicating - designed to infect other computers
	- the virus routine may be loaded into memory with the execution of a certain fille, then it may run some code to replicate itself to files of the same type 
- specific to cpu architecture, operating system, applications
- usually embedded into emails or as a macro 
- appending it at the end of a target file 

# Boot Sector Virus 
a type of virus that explicitly targets and contaminates a specific physical boot segment. A hard disks boot sector is replaced with malicious copies of code. The virus makes itself a **memory resident** meaning that it copies itself into the boot-loader 

