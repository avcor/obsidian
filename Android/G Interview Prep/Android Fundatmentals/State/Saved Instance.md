This topic is linked to [[Activity Lifecycle#`onCreate()`|onCreate]] 
Compose equivalent `rememberSaveable`
Bundle requires serialization on main thread and consumes system-process memory 
## `onCreate(savedInstanceState: Bundle?)`
**Creation Phase**
- This is an defensive API design - It is a clean separation between Initial launch and recreation launch
- It is always called, but can be null.
- views may not exist
- Used of for initialization 
### Why it is dangerous
- Views may not exist 
- View(Text) may be not resorted yet could risk of crashing  
## `onRestoreInstanceState(savedInstanceState)`
**Restoration Phase**
- It is a recreation after destruction this avoids mixing logic
- It exists because android needs a lifecycle callback that run only when state is being restored and view hierarchy is ready. 
- This give framework and developer guaranteed points  
	- Called only if state have to restore 
	- Bundle is guaranteed to non-null 
	- Views are already created - need to adjust or fix
	- Used for restoring state 

## `onSavedInstanceState(outState: Bundle)`
- Bundle with 1MB limit.  
- It is not a lifecycle callback, android call it when it believes that you might need state later.
- It is called before destruction but not guaranteed because android is resource constraint OS android may kill process immediately as freeing up memory is more important than saving state. If system waited to do that stuff it will serialize and write state it could freeze UI or ANR.
- Calling scenarios 
	- When it is called [[Configuration & Process death]] 
	- It is not called on finish() or press of home button 
- Why it is unreliable 
	- May not be called 
	- Heavy bundles may be dropped 
	- Serialization cost 
## What does android do automatically 
- `EditText` text
- `ScrollView` position 
### How it is automatically saved & restored
- For every view has id -> Android calls `view.onSaveInstaceState(): Parceable` 
- All views are stored in `SparseArray<Parceable>` then placed in activity bundle
- During recreation Walks down new hierarchy, matches views by ID then calls `view.onRestoreInstanceState(parceable)`
#### What happens 
**If there are no IDs or duplicate Ids** - state cannot be restored that can cause subtle bugs 

``` kotlin 
class MyAct: AppCompactActivity() {
	// this is the order 
	onCreate(savedInstaceState: Bundle?) {}
	onStart()
	onRestoreInstanceState(savedInstanceState)
	onResume()
}
```

