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
a type of virus that explicitly targets and contaminates a specific physical boot segment. A hard disks boot sector is replaced with malicious copies of code. The virus makes itself a **memory resident** meaning that it copies itself into the boot-loader. Very uncommon today and hard to actually implement due to builtin protections 

# Network Threats
network threats are harder to detect and prevent
- network protection systems are usually weaker 
	- no physical barriers once system is attached to the internet 

## Virus & Worm 
- both are malicious software 
- worm is a self replecating program that exploits network vulnerabilities to spread to other computers acriss a network 
### Worms
use spawn mechanisms (a standalone program)
- first was the morris worm (1988)
	- a specially crafted email with a specific sequence of characters. The worm could trigger a buffer overflow to create a downloader program 
	- execution of downloader program to fetch the actual hook program
	- loading major part of Morris worm and infecting system
	- volatile since it resides in memory 

## Port Scanning 
an automated attempt to connect to a range of ports on one or a range of IP addresses
- a technique used by hackers to find vulnerabilities in a business network 
- detection of answering service protocol 
- detection of OS and version running on system 
- to combat this, network monitoring or firewalls are needed - the aim of these is to make the system invisible to port scans

## Denial of Service 
- overload the targeted computer by preventing it from doing any useful work 
- DDOS comes from multiple sites at once 
- accidental - (CS students writing a bad fork() call)
- Purposeful 
	- DDOS attacks are orchestrated by controlling networks of compromised computers

# Cryptography
a method of protecting information and communications through the use of codes. 
A means to constrain potential senders (sources) and/or receivers (destinations) of messages
- based on secrets (keys)

## Asymmetric Encryption
public-key encryption based on a pair of two keys 
- public key - key used to encrypt data 
- private key - known only to individual user used to decrypt data in secret 

The goal for an encryption scheme such as RSA is to make encryption simple but description difficult without the key. 


let $C=M^e(modN)$ where:
- c - cyphertext
- m - plaintext 
- e - public exponent 
- N - modulus 

to encrypt:
$$M=C^d(modN) = M^{ed}(modN) = M^{k \phi(N)+1}(ModN) = M^1(modN)$$
for decrypting:
$$\phi(N) = (p-1)(q-1)$$ where phi is co-prime to N i think? 

# Authentication 
process of verifying a claimed identity of a user, device, or other entity in a computer system
- complementary to encryption 

### Hash function
- encode data with a hash function to generate a hash value 
- encrypt the hash value with a private key 
- send both the original data and the encrypted hash value to the recipient 
- verify the hash value by applying data to the same hash function with the public key

### Digital Certificates 
an electronic file that is tied to a cryptographic key pair and authenticates the identity of a website, individual, or organization 

- certificate usage: encrypting data, digitally signing documents or proving identity in secure communication 
- verification - the receiver can verify the authenticity of the certificate by checking the digital signature with the CA (certificate Authority's) public key 
- additionally, the receiver can authenticate the public key of the entity associated with the certificate 
- an entity (user) generates a key pair - public key and private key 
	- private key is used for decryption
	- public key is used for data encryption by a peer after its been authenticated by the CA 
- the entity submits a request for a digital certificate to a Certificate Authority (CA) 









