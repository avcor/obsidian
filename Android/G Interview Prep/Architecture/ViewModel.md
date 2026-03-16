- ViewModel holds [[State#UI state|UI state]]
- Repository own [[State#Domain State|domain state]]
- ViewModel adapts the domain state, converts it into UI state & survive config changes. It is a lifecycle aware adapter designed to keep UI-related state stable  while UI component are recreated. 
## Why it exists 
- UI objects are short-lived 
- State must survive configuration changes 
>`MVVM` is about state ownership and lifecycle boundaries.
## What is not guaranteed 
- Survival across process death 
- Business correctness 
- Persistance
> Guarantees exactly one thing  it needs to survive configuration changes but it is scoped to lifecycle owner.
## Why create after activity 
- Activity is framework object 
- ViewModel is a framework managed but app owned 
- ViewModelStore lives inside the activity.
- If ViewModel is created first -> ambiguity 
## Why not hold business logic
- Business logic should be 
	- Lifecycle agnostic 
	- Testable without android 
- If you put logic in ViewModel 
	- Bind rules to UI lifecycle 
	- Make Logic disposable 
	- Break reuse and testing 
> ViewModel coordinates, it does not decide

## When it fails 
> Using MVVM as a universal solution is wrong.
### 1. It becomes dumping ground 
- Example
	- Business rule 
	- Validation 
	- Navigation decision 
	- Retry logic 
- Symptoms
	- `validateUserInput()`
	- `decideNextScreen()`
- What breaks 
	- As screen grows, the view model becomes very large, hard to test and tightly coupled to UI flows 
	- Hard to test, as it needs android
		- ViewModel is testable as a class - but business logic inside it becomes architecturally fragile not technically fragile. 
	- Logic dies when screen dies 
	- Same rules can be duplicated in another ViewModel
## Alternatives
### Presenter 
- Presenter is lifecycle - agnostic | view model integrates with framework.
- It gives more control but has more boilerplate
### Redux
- It is centralized state | view model scoped state 
- Whole app observes one store but it is not aware of lifecycle | view model fits android lifecycle better.
## Process death
- It does not survive process death by design. View Model is scoped to a process and backed by purely memory heap. Android treat process death as hard reset, so all in memory object, including view model are wiped. 
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

