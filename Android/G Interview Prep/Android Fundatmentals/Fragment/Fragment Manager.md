## Fragment Manager Lifecycle 
The Fragment Manager ensures that fragment being added to activity is in a valid state (not currently in instance state). By queuing commit, system perform final check that ensure activity is not destroyed or paused as soon as you called `commit()`.
### How to override this behavior
- `commitNow()` 
	- This will execute transaction synchronously on main thread. 
	- You cannot use it if transaction is added to back stack. 
- `executePendingTransaction()` 
	- This tells the fragment manger to run all the pending fragment jobs waiting in queue immediately. 
**`IllegalStateException` is thrown if activity has saved its state and you call `commit()`**
## What it ensures / Why manager batch transaction 
### Goal
- Multiple fragment operations are applied together
- Lifecycle callbacks are dispatched in predictable order 
- Atomic UI update [[Fragment Transactions#commit#Case Study]]
- Avoiding partial State [[Fragment Transactions#commit#Case Study]]
- Asynchronous, frame-safe execution 
### Prevents 
- Fragment A removed, Fragment B not yet added [[Fragment Transactions#commit#Case Study]]
- Lifecycle callbacks interleaving incorrectly 
- UI logic observing impossible state 
