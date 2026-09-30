- There must be exactly one authoritative owner of a piece of state
- All consumer 
	- Read from it 
	- React to it 
	- Never mutate it directly 
## Guarantees 
- There is one authoritative owner of a piece of state 
- All reads are consistent with that owner 
- All mutation are serialized and intention
- The system cannot represent contradictory or impossible states at the same time
## Without SSOT
- Multiple Source of truth (MSOT)
	- Scenario where same data is stored or managed in more than one place, without synchronized master version. 
### Why it is dangerous 
- Primary danger is inconsistency.  If 2 parts of app have different idea of what the data is, UX breaks in unpredictable ways. 
	- [[Unidirectional flow (UDF)#Prevent#4. Ghost Update|Ghost Update]] 
	- [[Unidirectional flow (UDF)#2. Race conditions|Race Condition]] 
	- [[Unidirectional flow (UDF)#3. Stale Data|Stale Data]] 
### SSOT Rule 
>UI should reflect what is in database. If you want to change the UI database needs to be updated. Database pushes the update back up 
