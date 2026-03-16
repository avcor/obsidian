> It avoids [[#^381a89|hidden branch]] that complicates UI restoration. UI must be deterministic projection of state. 
## Exceptions 
- UI can react to state not the exceptions or side-effects 
	- If not 
		- UI cannot render deterministically.
		- UI must rely on off-signals (toast, callbacks)
	- If part of state 
		- UI can consistently render error 
		- Testing becomes deterministic 
## Problem with flags 
- When using flags such as `isLoading` `hasError` state can be in contradictory state where both are true. 
- Multiple flags can have number permutation and combination. **Sealed state** encodes invariant directly into the model. 
- Correctness of the state depends on developer discipline that person will update the state flag properly after consuming. 
## Exceptions / State 
> Exceptions represents unexpected control-flow interruptions 
- Exceptions are use useful at system boundaries 
	- Programming error 
- Exceptions are harmful at UI boundaries 
	- Not lifecycle-aware 
	- Cannot be rendered deterministically 
> Exceptions are control flow for developers, error state are use full for user.
## Sealed Class
### Modeling of Error state 
1. Transport Failure 
	- No Internet 
	- Timeout 
	- DNS failure 
2. Application failure 
	- 400/500 
	- Business validation failure 
3. Domain Failure 
	- User Blocked
	- Feature checks 
### Trade Offs 
- Boiler plate 
- Risk of over-modelling state - Sealed Class explosion
- Increased cognitive overhead
### Benefits 
- Compile time exhaustiveness checking 
- Prevention of unhanded states
- Stronger refactor safety - when new sate 

Hidden Branch - A control flow branch that affects UI but is not represented in a state model.    ^381a89
