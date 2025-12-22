### Process death
- `ViewModel` is memory construct process death clears memory so it cannot survive 
### Config changes
- It is scoped to `viewModelStoreOwner` activity recreation does not clear the store.
## SavedHandleState 
*Note - State must be simple and lightweight. For complex and large data use local persistence* 
- Google Introduced this because 
	- [[Saved Instance#`onSavedInstanceState(outState Bundle)`]] is unreliable, logic scattered across activity is bad architecture, **View Model need controlled persistence**. 
	- Needed a state container that survives process death without leaking Activity/Fragment.
	- The use depends on where the state is held and logic that it requires
		- For state that is required in business logic hold it in `ViewModel` and save it in `SavedStateHandle`
		- For state that is required in UI use [[Saved Instance#`onSavedInstanceState(outState Bundle)`]] or `rememberSaveable` in compose.
- It is **key-value map** that is attached to `ViewModel` that automatically save & restore pieces of state across process death. It is backed by **bundle** integrated by **`SavedStateRegistry`**.
- Saved State is tied to your task stack if your task stack goes away then state goes away. User initiated UI state dismissal scenarios saved state is not restored but it in system-initiated it will.
### Caution 
- `SavedStateHandle` does not persist immediately, observe continuously, sync after `onStop`.
	- This can cause subtle bugs when callback receives the data and stored in `HandleState` after `onStop`as app is in background, because data has not been saved because **`savedStateHandle` only guarantee to persist data written while owner is in `STARTED` or `RESUMED` state**. When user comes to foreground everything looks fine then after some time process dies in background and now state is mysteriously gone. 
	- In other words `SavedHandleState` persist data during `onStop` phase. 
- Hands values to system when asked
- Good for UI driven events.  It is lifecycle-snapshotted state, not a background-safe persistence mechanism. 
### How data is stored 
```
SavedStateHandle
|
SavedStateregistry
|
Bundle
|
Activity.onSaveInstanceState
```
That's why only bundled-supported types & small data only 
### Allowed data stored 
Int, Long, Boolean, String, Parcelable, Serializable, ArrayList, all these types are supported by bundle. 
Not Allowed - Bitmaps, Large list, Contexts, Views 

## Code
```kotlin
// activity 
val viewModel: StateViewModel = ViewModelProvider(this)[StateViewModel::class.java]

//ViewModel
class StateViewModel(  
    private val state: SavedStateHandle  
): ViewModel() {  
  /*
  set, get, contains, remove, keys, 
  LiveData, stateFlow 
   */ 
	savedStateHandle["count"] = 10
	val count: Int = savedStateHandle["count"] ?: 0
	val countFlow = savedStateHandle.getStateFlow("count", 0)
	val countLiveData = savedStateHandle.getLiveData<Int>("count")
	fun increment() {
	    savedStateHandle["count"] = countFlow.value + 1
	}
}
```

