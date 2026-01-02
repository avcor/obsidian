### Process death
- It does not survive process death by design. View Model is scoped to a process and backed by purely memory heap. Android tread process death as hard reset, so all in memory object, including view model are wiped. 
   - Persisting it automatically would be dangerous because view models has non serializable objects like repositories, coroutine, database.
   - Android separates concern 
	   - View Model - survives configuration changes 
	   - [[SavedStateHandle]] - survive process death 
	This forces developer to explicitly decide what state is worth restoring & preventing accidental persistence of large objects.
### Config changes
- It is scoped to `viewModelStoreOwner` activity recreation does not clear the store.
## SavedStateHandle
[[SavedStateHandle]]
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

