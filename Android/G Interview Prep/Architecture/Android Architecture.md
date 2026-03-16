> Android architecture is not about patterns - it is about surviving the lifecycle chaos, resources constraints and correctness under failure.
## Core reality 
What Android make Android 
- Kill app process without warning 
- Destroy UI objects frequently 
- Re-enter app in partially restored state 
> Architecture exists to impose order on chaos 
> It defines where state belongs in [[#Stability hierarchy|hierarchy]]
### Problems 
1. UI is not stable 
	- UI must be stateless or cheaply reconstructible. 
	- ***Protect state from unstable UI*** 
2. Lifecycle is hostile 
	- Architecture exists to decouple state form lifecycle.
	- ***Decouple business rules from lifecycle*** 
3. Memory & Process Death 
	- Architecture define 
		- What state is ephemeral
		- What state must survive death 
		- How restoration happens 
	- ***Survive process death and memory pressure***
4. Scale and entropy 
	- Architecture introduces 
		- Clear ownership 
		- Boundaries 
		- Invariants
	- ***Reduce cognitive load as system scale***
5. Failure is normal 
	- Model failure
	- Make error explicit
	- ***Make Failure explicit and manageable***
## Stability hierarchy 
- Process-independent storage 
- In memory state holder 
- UI
## [[Architecture]] Boundaries 