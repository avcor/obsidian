It is a simple side effect handler and run block of code after ever **successful recomposition.**
***It is not for long running task or suspend function.***
## Characteristics
- Runs after UI has been updated but before screen  is drawn
- **Synchronous** 
- If new composition enter while in `sideEffect` then the it will complete and previous UI is potentially is displayed. The second recomposition restarts and execution of `sideEffect` happens again.
## Use Case 
- Updating custom view property with compose state value 
- Updating analytical value 
- It guarantees that you will receive the absolute latest value before frame is displayed to user 

```kotlin 
@Composable
fun AnalyticsReporter(currentScreen: String) {
    SideEffect {
        analyticsManager.setCurrentScreen(currentScreen)
    }
}
```
## Why cannot we use it with [[launchedEffect]] 
- `launchedEffect` is primarily used to launch coroutine or call suspend function.
- There is an overhead of launching a coroutine. 
- Even if the block cancel and relaunches again on every composition it is still efficient as compared to `launchedEffect`
- `launchedEffect` is not designed for every composition but for initial or key changes  