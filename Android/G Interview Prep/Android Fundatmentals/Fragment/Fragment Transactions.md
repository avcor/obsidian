## commit
- `commit()` does not execute immediately on main thread, it schedule a job on main thread message queue.
### Why not synchronous 
#### Avoiding State Crashes (Re-entrant)
- Main reason is to prevent situation where you try to change the fragment state while it is in already middle of state change (like animation or lifecycle transition)
- If commit were instantaneous, you could trigger a fragment transaction inside another fragment's `onCreate()`. This might leave the UI inconsistent or can cause recursive loop of state changes that would crash the app. 
#### Main Thread synchronization
Everything related to view happens on main thread one at a time. 
- By putting transaction on main thread it ensures that transaction happens when main thread is ready and not busy processing a touch event or laying out view. 
- Also ensures that previous UI task (finishing or animating) are completed before a new fragment is swapped in.
### Fragment Manager Lifecycle 
The Fragment Manager ensures that fragment being added to activity is in a valid state (not currently in instance state). By queuing commit, system perform final check that ensure activity is not destroyed or paused as soon as you called `commit()`.
### How to override this behavior
- `commitNow()` 
	- This will execute transaction synchronously on main thread. 
	- You cannot use it if transaction is added to back stack. 
- `executePendingTransaction()` 
	- This tells the fragment manger to run all the pending fragment jobs waiting in queue immediately. 
**`IllegalStateException` is thrown if activity has saved its state and you call `commit()`**

## commitNow
- It will execute the transaction immediately on current thread. 
- You cannot use it for `addToBackStack()` with `commitNow()`
	- If there are other asynchronous commit waiting in queue, executing a back stack transaction would mess up the order of history 


## commitAllowingStateLoss
- It is similar to commit asynchronous but it will not throw an exception if called after state is saved. 
- Fragment transaction you have committed after system kills the app, will simply disappear.
- It is used for non critical UI changes where missing fragment wont break app logic 

Next - [[Fragment Transactions code]]