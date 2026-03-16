> Architecture is the set of constraints that intentionally limit where certain kind of decision can be made, so system remains correct as its grows.
>  This allow to change the part of the system independently while preserving the system invariant.  

> Think of architecture as a way to protect invariant of the system. 

- Ownership boundaries 
- Rules about who can change what 
- Guarantees about state consistency 
## Tight Coupling 
- When UI code knows where data comes from
- When Business logic knows how data is stored
- What it causes - 
	- Cost of change 
	- Risk of regression 
	- Difficulty of testing 
	- Chance of state inconsistency
## Problems 
- Without 
	- Logic can be spread among UI, ViewModel, callbacks 
	- Bugs appear in certain sequence 
	- Fixing one thing breaks another 
	- Fear of refactoring 
	- Flags everywhere
- With 
	- Make invalid state unrepresentable 
	- Localize reasoning 
	- Prevents accidental coupling 
## Guarantees 
> It does not guarantees correctness of business logic, but structural correctness of system. 
- Guarantees 
	- Clear ownership of state 
	- Predictable data flow 
	- Limited mutation points 
	- Easier reasoning under change
	- Error are handled explicitly 
## Trade Off
- It is upfront complexity and slower initial development.
- It buys long term stability and scalability.