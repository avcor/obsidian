## Task
It is a stack of activities representing user's journey.
*Task belong to System, not your process.* 
Task has - Root Activity  & Own history 
- Task is not an app, app can have multiple task. (LIFO)
	- Task is not the same as app because tasks are user-facing navigation container, while app is package and process identity.
	- A single app can contribute activities to multiple task, and task can outlive the app.
	- The system remembers the logical navigation history.
	- Task still appear in `Recents`
	- Android knows which activities were in stack.
### Why Android allow multiple task 
Android allow multiple task per app so different entry points can represent independent user goals without forcing single linear navigation history.
- It is need to have independent user journey (Deep links, notification)
- Document style apps (multiple documents)
- Better multi-tasking and recent behavior. 
- Re-entry into different parts of the app.
### Back Stack 
It is the state meta data that manages the history of screen user have visited in the task. (not a heap memory )
System restore the stack not your objects 
It survives the configuration changes but not the process death.