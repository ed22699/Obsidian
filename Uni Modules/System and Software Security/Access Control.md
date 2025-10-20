---
tags:
  - Lesson
---
![[Screenshot 2025-10-20 at 14.05.14.png|400]]
- different users have different tiers of access
- stages
	- identification: present identity
	- authentication: present photo ID
	- enforcement mechanism: check ID by security agent
	- authorisation: staff member access
![[Screenshot 2025-10-20 at 14.10.58.png|400]]
- ability to allow only authorised users, programs of processes system or resource access
- granting or denying, according to a particular security model, of certain permissions to access a resource
- an entire set of procedures performed by hardware, software and administrators, to monitor access, identify users requesting access, record access attempts and grant or deny access based on pre-established rules
![[Screenshot 2025-10-20 at 14.11.57.png|500]]
- domains and applications
	- social networks
	- web browsers
	- operating systems
	- firewalls
## Access control methods
- access control methods
	- *mandatory access control (MAC)*
		- systems administrator sets the policy as to who can access what
		- typical implementations that you might see:
			- SELinux: NSA's patches for Linus to add a MAC
			- AppArmour: Canonical's simplified MAC system based on paths
			- TOMOYO: another simplified system based on paths
		- policies can be applied to more than just files
			- e.g. web browser can access files in the downloads folder only
		- rules are enforced on every attempted access, not at the discretion of any system user
	- *discretionary access control (DAC)*
		- scheme in which an entity may enable another entity to access some resource
		- often provided using an access matrix
			- one dimension consists of identified subjects that may attempt data access to the resources
		- each entry in the matrix indicates the access rights of a particular subject for a particular object
		- rule enforcement may be waived or modified by some users
	- *role based access control (RBAC)*
		- widely used security framework claimed to be especially appropriate for commercial settings
		- unlike access control policies that assign permissions to subjects, RBAC associates permissions with functions/jobs/roles within an organisation
		- a role is a collection of job functions, e.g. manager, auditor, janitor
			- associate permissions with job functions
				- each job defines a set of tasks
				- tasks need permissions
				- permissions define a role
			- bank teller: 
				- read/write to client accounts
				- cannot create new accounts
				- cannot create a loan
			- role defines only the permissions allowed for the job
		- an individual has
			- a set of authorised roles, which it is allowed to fill at various times
			- a set of active roles, which it currently occupies
		- roles have an associated set of transactions, which are the activities that someone in that role is permitted to carry out
			- the set of transactions can be organisation specific: open an account, check cash
		- three primary rules
			- *role assignment*: a subject can execute a transaction only if the subject has an active role
			- *role authorisation*: a subject's active role must be an authorised role for that subject
			- *transaction authorisation*: a subject can execute a transaction only if the transaction is authorised for one of the subject's active roles
	- *attribute based access control (ABAC)*
		- access rights are defined upon attributes
		- the users' identities are not used anymore to define access rights
		- to get access, users need to prove their possession of the required attributes
			- users are authenticated to the server to prove their rights
		- ABAC is an extension of RBAC where users' roles are more generalised
		- user access rights are expressed using a set of attributes
- multiple access control policies are not mutually exclusive
	- system may implement two or even three of these policies for some or all types of access
- access control matrix (ACM) is a matrix of all principals and objects
	- matrix entries describe the permissions for subjects, objects, and operations
	- can determine
		- who can access an object
		- what objects can be accessed by a subject
		- what operations a subject can perform on an object
	- *problem*: maintaining such a matrix can be difficult
		- if the matrix is corrupted then all controls is lost
![[Screenshot 2025-10-20 at 14.20.53.png|500]]
![[Screenshot 2025-10-20 at 14.21.52.png|500]]
- *Access Control Lists (ACLs)*
	- we do not want to store one massive matrix
	- instead we can store each column of the matrix with the object it refers to 
	- e.g. (O2,(J,RW), (S2,R), (S3,R))
![[Screenshot 2025-10-20 at 14.39.32.png|500]]
![[Screenshot 2025-10-20 at 15.03.41.png|500]]
## Access Control in Unix/Linux
- Unix/Linux/Mac use ACL, with groups
- "uid" set when you log on
- Linux Kernel then dynamically enforces the ACLS
- ls -l displays files with their ACL
- `root` owns everything
![[Screenshot 2025-10-20 at 15.05.38.png|300]]
![[Screenshot 2025-10-20 at 15.05.59.png|400]]
## Sandbox
- sandboxing is a cybersecurity procedure in which you run code, analyse it, and code in a secure, enclosed environment on a system that resembles end-user working environments
	- is intended to prevent the potential threat from entering the network and is commonly used to scrutinise unknown or non-secure code
- often need to run buggy/untrusted code
	- programs from untrusted internet sites: toolbars, viewers, codecs for media player
	- old or insecure applications
	- legacy software
- *aim*: if application misbehaves kill it
![[Screenshot 2025-10-20 at 15.09.14.png|500]]
![[Screenshot 2025-10-20 at 15.09.35.png|500]]
- *benefits*:
	- prevents zero-day attacks
		- exploit unknown security flaws
		- highly hazardous because manufacturers cannot issue patches unless they fully comprehend the exploited vulnerability
		- sandboxing software isolates these
			- there is no assurance that it will prevent zero-day manipulations, most often works for damage limitation by distancing the potential danger from the remainder of the network
	- enhances other security programs
		- is an excellent compliment to specific other security software
			- action monitoring programs
			- antivirus programs
		- shields against spyware strains that your virus protection may struggle to detect
	- helps examine presumably malicious programs for threats
		- if dealing with new vendors or untrustworthy software sources you can try out the application before incorporating it
	- allows rigorous software tests before they are released
		- software changes should be thoroughly tested before they are released to the public
		- sandboxing can be used to test new code for possible risks before it officially launches
			- has a vital role to play in application security
## How to sandbox any program
- virtual machines
	- VirtualBox or VMware
	- creates virtual hardware devices that ut uses to run an operating system
	- entire operating system is essentially sandboxed, as it does not have access to anything outside of the virtual machine
- using other tools
	- Sandboxie
	- Bufferzone