
## Structured Concurrency 
- It ensures that coroutines are launched in defined scope, and the child coroutines are tied to lifetime of parent  coroutine and its scope. 
- If parent scope is cancelled then all its child will be cancelled

## `CoroutineScope`
It defines the scope of coroutines. It defines the boundary within which coroutines are executed

```kotlin
CoroutineScope(Dispatchers.IO).launch {
	// scope is asscociated till it is executing 
}

GlobalScope.launch {
	// linked to application lifecycle 
}

viewModelScope.launch {
	// attached to viewModel, cancel automatically onCleared() of viewModel 
}

lifecycleScope.launch {
	// attached to lifecycle of activity, fragment, cancelled when lifecycle is destroyed
}
```

## `repeatOnLifecycle`
Lifecycle aware coroutine builder that ensures coroutines only collects or run code only when lifecycle is in a specific state. 

```kotlin
lifecycleScope.launch {
    repeatOnLifecycle(Lifecycle.State.STARTED) {
	    // this block runs only when lifecycle >= STARTED
    }
	repeatOnLifecycle(Lifecycle.State.RESUMED) {
	    // runs only between onResume() and onPause()
	}
}
```
### Working 
- coroutines starts but suspended immediately 
- when lifecycle enter `STARTED` (`onStart`) - launches a new coroutine inside. 
- when lifecycle goes below `STARTED` (`onStop`) inner coroutine is cancelled
- when lifecycle comes back `STARTED` launches new coroutine
*Note - Referring to [[Lifecycle - aware components]] as lifecycle above* 

### What problem does it solves 
- It prevent updating the UI when view is destroyed, causing a crash or memory leaks. 
- Normal `lifecycleScope` cancels `onDestroy` and does not care about `onStop` or `onPause`
- `launchWhenStarted`
	- pauses the coroutines 
	- keeps open channel in memory 
	- if producer keeps emitting data, it buffers up - possible memory leaks 
