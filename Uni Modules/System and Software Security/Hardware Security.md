---
tags:
  - Lesson
---
## Rootkit
- purpose
	- give attacker a permanent root access to a system
	- hide its presence
	- steal information 
	- allow remote code execution
- typical steps
	- initial intrusion (exploit remote execution)
	- open remote access (reverse shell)
	- privilege escalation
	- download the malicious payload (rootkit)
	- install rootkit
	- perform malicious action on command
		- DDOS
		- Steal data
		- etc
![[Drawing 2025-12-12 15.30.33.excalidraw|650]]
- three techniques:
	- modify the kernel code
	- hooking modify where certain functions point to
	- modify data structure, e.g. active process list
### Types of rootkit
- Application rootkit
- Kernel rootkit
- Virtualised rootkit
- Bootloader rootkit
- Hardware and firmware rootkit
- can be prevented/detected by going at least one layer down
## Attack Surface
- is all the possible ways for an attacker to compromise a system
	- users
	- network
	- operating systems
	- software 
	- hardware
- sandboxing prevents application from passing rootkit out onto the operating system. e.g. Browser sandbox
- trusted execution environment prevents passing rootkit into application. e.g. SGX enclave
	- Trusted computing base (TCB)
		- looks are what part of the system you need to trust in order to achieve objective