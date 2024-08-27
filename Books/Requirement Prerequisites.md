- The goal of preparation is risk reduction. The most common project risks are poor requirements and project planning
- you need to complete requirements and planning before beginning code as error will be more costly with requirements are not defined
- iterative approaches reduce the effects of poor planning however do not eliminate them

**Do sequential when:**
- requirements are fairly stable
- design is straightforward and fairly well understood
- development team is familiar with the applications area
- project contains little risk
- long-term predictability is important
- cost of changing requirements, design, and code downstream is likely to be high
**Do iterative when:**
- requirements are not well understood or you expect them to be unstable 
- design is complex, challenging, or both
- development team is unfamiliar with the applications area
- project contains a lot of risk
- long-term predictability is not important
- the cost of changing requirements, design, and code downstream is likely to be low

- problem definition is writing describing the problem. This should not include technical terms and should be in the users perspective, it should not hint at any solutions or try to guide people towards a certain solution, this should only be 1 to 2 pages

**Requirements are important as:**
- they keep the user in the loop, they can look over these requirements and agree to them, undefined requirements can result in programmers assuming requirements during the coding process. Explicit requirements help show what the user wants.
- reduces arguments between programmers as they can refer back to these requirements 
- leads to less required changes
- the users requirements will change around 25% during construction which results in 70-85% of the rework on a typical project

## Handling requirement changes during construction
- use requirements checklist at the end of the section to assess the quality of the requirements
- make sure everyone knows the cost of requirements changes
	- if user has a new feature say "sounds like a great idea. Since it's not in the requirements document, I'll work up a revised schedule and cost estimate so that you can decide whether you want to do it now or later", this usually makes users think this through more
- set up a change-control procedure
- use development approaches that accommodate changes
- dump the project
- keep your eye on the business case for the project (is the new feature actually beneficial to the end goal)
Checklist Requirements: p42-43

## Architecture Prerequisite
important as it determines the conceptual integrity of the system in turn determining the quality of the system. It partitions work so that multiple teams can work independently
- first describe in broad terms
### Major Classes
- identify responsibilities of each major class and how it will interact
- describe class hierarchies
- describe what other designs were considered and why this was chosen
- aim to specify the 20% of classes that make up 80% of the system behaviour 

### Data Design
- justify how data is stored and why the alternatives were not chosen
- show the structure of the database and ensure only once subsystem or class is used to access the data
### Business Rules
- if architecture is dependent of specific business rules, specify them e.g. if customer info should be no more than 30 seconds out of date
### User Interface Design
- specify whether it is a GUI, command line interface, etc
- architecture should be modularised so that a new user interface can be substituted without affecting the rest of the program
### Resource Management
- plan for managing scarce resources such as database connections, threads and handles.
- memory management
- estimate resources used for nominal and extreme cases
### Security
- describe approach to design-level and code-level security
- include approaches to handling buffers, rules for handling untrusted data, encryption, level of detail contained in error messages, protecting secret data that's in memory, etc
### Performance
- goals should be specified, can include resource use
- provide estimates 
### Scalability
- describe how the system will address growth in number of users, number of servers, number of network nodes, number of database records, size of database records, transaction volume, etc
- if not expected to grow make assumption explicit 
### Interoperability
- if expected to share data or resources describe how
### Internationalisation/Localisation
- determine if multiple languages will be used, which character sets will be used etc
### I/O
- how it is read, if it is look ahead, look behind or just in time reading
- level at which errors are detected at field, record, stream or file level
### Error Processing
- corrective or detective?
- active or passive?
- how does the program propagate errors?
- what are the conventions for handling error messages?
- how will exceptions be handled?
- inside the program, at what level are errors handled?
- what is the level of responsibility of each class for validating its input data?
- do you want to use your environment's built-in exception-handling mechanisms or build your own?
