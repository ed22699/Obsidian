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
- sandboxing prevents application from passing rootkit out onto the operating system. e.g. Browser sandbox, this reduces the attack surface
- trusted execution environment prevents passing rootkit into application. e.g. SGX enclave
	- Trusted computing base (TCB)
		- looks are what part of the system you need to trust in order to achieve objective
		- use trusted hardware as the base of trusted computing, rootkits could be in other applications or the OS itself but the hardware is trustworthy
![[Pasted image 20251212164045.png|400]]
## Trusted Platform Module (TPM)
- trusted computing group
	- Microsoft, Intel, IMB
- promotes standard for more trusted computing
	- additional chip on the motherboard called TPM
	- used for
		- disk encryption
		- system integrity
		- password protection
- requirements
	- achieve trust if we can verify the system has booted correctly
	- assume the PC hardware has not been modified
		- key function is in the hardware TPM
	- need to monitor the boot process
		- initial boot measure by the core root of trust (CRTM)
			- first piece of BIOS that executes on the main processor during the boot process
			- On trusted platform is implicitly trusted to bootstrap the process of building a measurement chain for subsequent attestation of other firmware and software that is executed on the computer system
		- hash the BIOS, store results in TPM, start the BIOS
		- BIOS do its job, load the next stage, hash it store in TPM
![[Pasted image 20251212155821.png|400]]
### TPM Registers
- platform configuration registers (PCRs)
	- used to store platform integrity metrics
	- holds a summary of a series of value
		- not the entire chain of hash (this can be infinite)
- a PCR register is extended
	- PCR = HASH(PCR | new measurement)
	- shielded TPM locations (i.e. cannot be modified from outside)
	- measurement are provided by software
### Remote attestation
- attestation is a mechanism for software to prove its identity
- goal is to prove to a remote party that your operating system and application software are intact and trustworthy
- verifier trusts that attestation data is accurate because it is signed by a TPM whose key is certified by the CA
![[Pasted image 20251212164626.png|500]]
- remote attestation tells you
	- positive result
		- correct memory content
		- good device
	- negative result
		- malfunctioning device
		- malicious device
	- no response
		- malfunctioning device
		- malicious device
- PCR cannot be modified
	- only reset at reboot
- TPM contains a key used to sign the attestation 
- verifier
	- verify the TPM certificate/key
	- verify the PCRs
- attestation
	- PCRs value
	- sign(PCRs, challenge\[nonce\])
## Intel SGX
- an attacker can compromise
	- user space
	- operating systems
	- hardware
- *solution*:
	- execute code in its own secure enclave
		- run application within some isolation unit so it cannot be affected by the OS
			- do not trust the OS or the VMM/hypervisor
			- only need to trust the hardware
			- reduce attack surface
![[Pasted image 20251212165452.png|400]]
- SGX preventing memory snooping attack
	- security boundary is CPU
	- data unencrypted inside the CPU
	- data outside the CPU is encrypted
	- external memory reads and bus snooping only see encrypted data
	- this means snooping cannot occur on the memory but or in the system memory
- SGX programming environment
	- enclave has its own code and data
		- provides confidentiality and integrity
	- controlled entry point
		- can enter enclave code only at specific point
		- enclave execution takes over
![[Pasted image 20251212165909.png|200]]
- SGX application flow
	1. define and partition application into trusted and untrusted part
	2. app create enclave
	3. trusted function is called
	4. code in enclave process some secret 
	5. trusted function returns
	6. app continue as normal
## ARM Trustzone
- has its own processor, RAM address and devices, etc
- used for:
	- digital right management
	- secure banking 
	- multi-factor authentication
![[Pasted image 20251212170200.png|400]]