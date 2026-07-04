-  Atomicity  
	- All or nothing rule. If one part of transaction fails then entire transaction is rolled back as if nothing happened 
- Consistency 
	- Ensures that a transaction bring the db from one valid state to another valid state. 
- Isolation 
	- If multiple people are changing the same data at exact same time, transaction ensure they are do not interfere with each other. 
- Durability 
	- If transaction is committed it stays saved. 

## When to use them 
- Reserving a seat and processing a payment at same time. 
