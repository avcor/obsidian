Overview - it is a key value store of bundle whose job is
When the process dies, tell me what small pieces of state should I need to restore 

- It is a coordination mechanism that allows multiple independent component to contribute there small pieces of state into a single saved-state snapshot, and restore them later. 
- It is owned (or lives in) by activity / fragment 
- Used by child components 
- It does not know nothing about `LiveData`, `ViewModel`, `Compose`
## Core Responsibility 
- Let component register [[#State provider]]
- Collect those bundle during [[Save Instance#`onSavedInstanceState(outState Bundle)`|onSavenstanceState]] 
- Give them during recreation 
## Flow
- System kills the process
- Activity gets on `onSavedInstanceState`
- SavedStateRegistry
	- Iterates over registered providers 
	- Calls each one 
	- Collects Bundle
*Note - You do not call providers `SavedStateRegistry` does*

## Why exist  & Problem earlier
- There was only one bundle `onSaveInstanceStat(outState: Bundle?)` and everyone competed for it - views, fragment , libraries.
- Problem it faced 
	- key collision 
	- no owner ship clarity
- Android needs decentralized state saving and central snapshotting
## State provider
It is a function that knows how to save its own state in `Bundle` when system asks 
`() -> Bundle`
It is called only on `onSavedInstanceState` 
### Question
Q. Why Providers instead of passing a bundle directly?
- State may change over time 
- Registry wants latest state 
- Providers lets registry to call at last possible moment - by saying 'give me your final answer before death'

## Code Example 
Raw code with no View Model 
```kotlin
class MyActivity : ComponentActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        savedStateRegistry.registerSavedStateProvider("counter") {
            // this function is state provide 
            Bundle().apply {
                putInt("value", counter)
            }
        }

        val restored =
            savedStateRegistry.consumeRestoredStateForKey("counter")
        counter = restored?.getInt("value") ?: 0
    }

    private var counter = 0
}
```