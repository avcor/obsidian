It store the latest value without restating the effect.

## Characteristics 
- It creates the reference to most recent value of state 
- Reference is updated synchronously during the recomposition and it does not restart any `sideEffect` like [[launchedEffect]] or [[disposableEffect]]
## Use case 
It can be used in long running task but requires the latest reference to object.

## Ideal example
``` kotlin 
@Composable 
fun Timer(onTimeout: ()->Unit) {
	val currentFn by rememeberUpdateState(onTimeout)
	
	LaunchedEffect(Unit) {
		delay(3.seconds)
		currentFn.invoke()
	}
}
```

## Why not use [[remember]]
```kotlin 
@Composable 
fun Timer(onTimeout: ()->Unit) {
	val currentFn by rememeber(onTimeOut) {onTimeOut}
	
	LaunchedEffect(Unit) {
		delay(3.seconds)
		// it will still use the old reference 
		currentFn.invoke()
	}
}
```
