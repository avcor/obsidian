*Note - It is a composable function* 
## Life
- It is used to launch a coroutine within a scope of composable function 
- It is launched when composable first enters the composition or when the keys change 
- If composable is disposed (or leave the composition) or the key changes then the current running coroutine scope is get cancelled. A new coroutine is launched if composable remains in the composition 

## Use case
Long running operations or task that is tied to the lifecycle of the composable. 
E.g. 
- Showing Snackbar 
- Implementing animation or timer 
- Suspend function api call 

```kotlin 
@Composable
fun UserProfile(userId: String) {
	// Use Unit to run it one time 
	var text by remember {
		mutableStateOf("helllo")
	}
    LaunchedEffect(key1 = userId, key2 = text) {
	    delay(2.seconds)   
	    launch {}
    }
    LaunchedEffect(userId, Unit, false, true ) {
    }
}
```