##  standard (default)
- Every launch create new instance and pushed at the top
	- Catch 
		- Duplicate deep links or notification if fired repeatedly
	- Use Case 
		- Normal flows 

##  singleTop
-  If activity is already at top, reuse it. Otherwise create a new instance
	- For existing instance `onNewIntent()` will be called instead of `onCreate()`
	- Use Case 
		- Notification clicks 
		- Avoid duplicate screen at top 

## singleTask
- Only one instance per task, if exist system will clear everything above it.
	- Activity becomes task root & `onNewIntent()` is called. 
	- Use Case 
		- Auth Screen 
		- Deep links target 
### Why it feels buggy 
Because it silently clears above activities, break expected back navigation and reuse existing instance via `onNewInten()`. Which might forget to handle correctly.

## singleInstance
- Activity lives on its own [[Task & Back Stack#Task|Task]]
	- Rare in normal apps.
	- [[Task & Back Stack#Task#Why Android allow multiple task]]
	- Misusing it can fragment the user experience by creating unexpected task, breaking back navigation and causing confusing behavior in recent. 
	- Note - just adding this flag wont create different entry point in recents app drawer
