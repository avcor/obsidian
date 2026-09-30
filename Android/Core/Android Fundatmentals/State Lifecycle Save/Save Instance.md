This topic is linked to [[Activity Lifecycle#`onCreate()`|onCreate]] 
Compose equivalent `rememberSaveable`
Bundle requires serialization on main thread and consumes system-process memory 
## How to decide to save 
- Is it visible to user ?
- Can user reasonably expect it to be restored ?
- Is it safe to restore ? (pending request)
- Is it derived or source of truth ?
	- Derived -> do not save  
	- Transient -> do not save 
> Saved state should only contain minimal, user-visible UI continuity data, never business state or derivable data.
> It is for **restoring what the user sees**, not what the app was doing internally.
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
- It exists because android needs a lifecycle callback that run only when state is being restored and view hierarchy is ready. 
- This give framework and developer guaranteed points  
	- Called only if state have to restore 
	- Bundle is guaranteed to non-null 
	- Views are already created - need to adjust or fix
	- Used for restoring state 

## `onSaveInstanceState(outState: Bundle)`
> It is best-effort because Android treats state saving as a user-experience optimization, not a correctness guarantee.

> Bundle size to 1 MB because saved state is marshaled through Binder IPC. Binder has strict size limit and large bundle would block the main thread. This limit enforces the invariant that state saving must fast and predictable. 
 
- It is not a lifecycle callback, android call it when it believes that you might need state later.
- It is called before destruction but not guaranteed because android is resource constraint OS android may kill process immediately as freeing up memory is more important than saving state. If system waited to do that stuff it will serialize and write state it could freeze UI or ANR.
- Calling scenarios 
	- When it is called [[Configuration Changes]] 
	- Before backgrounding in some case
	- It is not called on finish() 
- Why it is unreliable 
	- May not be called 
	- Heavy bundles may be dropped 
	- Serialization cost 
### When 
- Configuration changes 
- Before back grounding in some cases 
### When Skips 
- Killing under memory pressure 
- User force stop the app 
- When app crash 
### observation 
`onSavedInstanceState` is called after `onStop()` even when we navigate to new screen but does not call `onRestoreInstanceState()` when we come back 
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

