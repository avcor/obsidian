> It is a data structure that used to record the fragment transactions 

- It Is managed by Fragment Manager 
- Exists inside one activity 
- Replays fragment transaction, not lifecycle history. 

## Question
- If fragment A is recreated ?
	- If A is retained -> not created 
	- If A was destroyed -> recreated 
	- It does not guarantee reuse of same fragment object