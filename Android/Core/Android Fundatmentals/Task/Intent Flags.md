[[Launch Mode]] are static (manifest)
[[Intent Flags]] are dynamic (runtime)

1. `FLAG_ACTIVITY_NEW_TASK`
	- Start activity in a new task, required when launching from non-Activity context
	- Similar to [[Launch Mode#singleInstance|singleInstance]]

2. `FLAG_ACTIVITY_CLEAR_TOP`
	- Similar to [[Launch Mode#singleTask|singleTask]] 

3. `FLAG_ACTIVITY_SINGLE_TOP`
	- Similar to [[Launch Mode#singleTop|singleTop]]
