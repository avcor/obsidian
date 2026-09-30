Go through [[Lifecycle]]
First activity is not completely stopped before second one is created. If two activities are in same process then 
A `onPause()` - B `onCreate()` `onStart()` `onResume()` - A `onStop()`
## onCreate() 
**Where Activity is initialized not interacted with*
- Activity instance is being created & system is allocating resources.
	- Views being inflated
	- Dependencies being initialized 
		- Associate the activity with a `ViewModel`
		- Instantiate some class scoped variable
	- Startup logic that happens only once for entire lifecycle of activity
- No UI interaction are allowed because UI has not be drawn and input cannot be possible
- Receives [[Save Instance|savedInstanceState]] if new null otherwise bundle from previously saved state.
### what should not be done
- Heavy computation 
- Anything that is depended on user interaction 
- UI related network call 
## onStart()
**Visibility without interaction**
- App prepare the activity to enter foreground, still not ready for user input, but window is attached.
- Why it is needed 
	- Visibility and interaction are different guarantees
		- Examples 
			- Split screen 2 activities can be visible but only one can be interactive
	- When activity goes fully hidden & then comes back to foreground it need to come `onStart()` 
- It exists to show UI, delay inputs, maintain consistent interaction rules 
### Uses 
- Initialize listeners such as camera and check for permission.
- Good places to start animation that should run as soon as user sees the screen. 
## onResume()
- Activity comes to foreground (focus) and remains in this state until it goes away from focus.
- User now can interact because touch events can happen, and keyboard input works.
(look at split screen example in [[#onStart()]]
### Uses 
- If user has focus then only start camera preview 
## onPause()
- `onPause()` is part of the critical path for the next Activity’s interaction
- exists to immediately revoke input ownership so Android can safely grant focus to another activity.
- Activity is no longer in foreground (focus) because
	- Dialog come foreground
	- In Multi window does not have focus 
	- Another activity is coming at top
- It does not offer enough time frame to
	- save user data
	- make network calls
	- execute database transactions.
- What should happen over here 
	- Stop animations 
	- Pause camera 
### What should not be done 
- Disk I/O
- Networks calls 
- Heavy cleanups 
#### Reason for this 
- If you block `onPause()` next activity will feel slow.
- That's a system violation.
## onStop()
- Activity is fully hidden therefore no UI
- System may kill activity anytime after this
- Activity object is kept resident in memory maintaining all states and member information
- It offers better time to save information in db 
- When it called 
	- When activity is no longer visible
	- New activity covers the entire screen 
	- Also when it finishes running and about to be terminated
## onDestory()
- This is the best effort clean up 
	- why 
		- Android does not guarantee it will be called if system tries to kill the process, due to memory constraints, when app is in background.
		- Or process will survive long enough 
- It is called before the activity instance is removed
	- User dismissing the activity or `finish()` is being called
		- Almost always, but **not guaranteed**.
			- System or Native crash
	- Due to configuration changes rotation or entering multi-window mode 
- What should be used for then 
	- Final safety net 
	- Memory leak prevention 
	- Defensive programming 
	- `binding = null` could be a possible case in destroy method
- User `viewModel.onCleared()` if activity is not being recreated. 
- Use `isFinishing()` can be used to distinguish between the recreation or destroyed 
