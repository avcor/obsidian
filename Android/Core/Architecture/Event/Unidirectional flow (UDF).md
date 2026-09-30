- Data flows in one direction only 
- It creates clarity 
## Why this matters 
- For UI state, you can answer 
	- What caused this?
	- Which event produced it ?
	- Which logic handled it ?
- What it helps 
	- Debugging is easier 
	- Testing becomes predictable 
	- Side effects are isolated 
### Predictability 
Is something goes wrong with UI, we have to look at only one place, state producer. 
### Consistency 
We can prevent ghost updates. UI never decided what to show, it just reflects the latest state packets.
## Prevent
1. Temporal bugs 
	- State is read in middle of partial update. UI shows combinations that should never exists. 
	- UDF forces 
		- Event - complete state calculation - emission 
		- No mid transition reads 
2. Race conditions 
	- Two async operations mutate state independently. Final UI depends on timing not logic
	- UDF prevent this by 
		- Centralizing mutations 
		- Making updates seqentials and predictable 
3. Stale Data 
	- Your update profile pic on one screen, but on other screen it is showing previous pic because it is reading from different cache. 
 4. Ghost Update
	- User toggles the button, UI is updated but DB fails. Later user returns toggle is gone. 

## Trade Offs
- UDF increases boilerplate and requires discipline
- May slow iteration speed 
