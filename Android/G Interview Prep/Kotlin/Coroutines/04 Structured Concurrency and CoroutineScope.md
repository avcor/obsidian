
## Structured Concurrency 
- It ensures that coroutines are launched in defined scope, and the child coroutines are tied to lifetime of parent  coroutine and its scope. 
- If parent scope is cancelled then all its child will be cancelled

## CoroutineScope
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


TODO 
Repeate on lifecycle 
