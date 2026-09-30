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
### Case Study 
Lets assume that batching does not exist. You do Remove `Fragment A` and add `Fragment B`. It will be executed immediately. `Fragment A` is destroyed, `Fragment B` not yet added  UI is blank for a frame. 
This will result in 
- Invalid UI logic 
- Illegal state access 
- Can break lifecycle assumption
```
Step 1: remove A → A.onPause(), A.onStop(), A.onDestroyView()  
Step 2: (gap here ⚠️)  
Step 3: add B → B.onCreateView(), B.onStart(), B.onResume()
```
What batching ensures Old UI exist or New UI exist. Never half applied state. This is **Atomic UI updates**.
## commitNow
`commitNow()` trades lifecycle safety for immediacy. It is dangerous because it can trigger 
### Problems
- UI hierarchy may be mutated during measurement/layout
- [[#commit#Why not synchronous#Avoiding State Crashes (Re-entrant)]]

This is why Google documentation says
> Avoid `commitNow` unless you know exactly what you’re doing

Callbacks at unexpected time 
- It will execute the transaction immediately on current thread. 
- You cannot use it for `addToBackStack()` with `commitNow()`
	- If there are other asynchronous commit waiting in queue, executing a back stack transaction would mess up the order of history 
### Ability it gives 
- Offscreen fragments (ViewPager)
- Back Stack fragment 
- Memory Optimization
### Why it exists 
#### Mostly for framework logic
- Use
	- Android framework code may need to - Add a fragment, Immediately query it, Immediately interact with its child `FragmentManager` or view 
- If not used 
	- Fragment would not exist yet
	- Framework would have to rely on callbacks 
	- Initialization order becomes unpredictable 
	- Framework might not rely on later 
- Example
	- `FragmentContainerView`
		- It may need to attach a fragment immediately 
		- The system expects the fragment to exist synchronously
		- What will break if this not happen 
			- Layout pass could happen without Fragment content 
			- Measurement/Layout would be wrong 
			- First drawn could be broken 
#### Setup code before first draw 
- Scenario - An activity which contains a container and want a initial fragment 
- What I want - Fragment to exist before first frame, No visible transaction, no flicker, no bank state. 
- why not `commit()` - transaction is queued, first frame may be empty, fragment may appear in next frame.
- What it ensures() - Fragment is fully attached, Views exist, first is complete 
##### Constraints 
- No other fragment exists 
- No back stack is involved 
- No lifecycle transition mid-frame 
## commitAllowingStateLoss
- It is similar to commit asynchronous but it will not throw an exception if called after state is saved. 
- Fragment transaction you have committed after system kills the app, will simply disappear.
- It is used for non critical UI changes where missing fragment wont break app logic 

Next - [[Fragment Transactions code]]

## Scenario 
1. What will happen if there is lifecycle transition is going on then I call `commitNow` on another fragment replacing it in a single holder container. 
	- Crash - `IllegalStateException` `FragmentManager` is already executing transactions.
	- Callbacks back are fired out of order - Observer not registered, resource leaked.
	- View hierarchy corruption - Bank screen, crash in layout, `IllegalArgumentException: View not attached to window`