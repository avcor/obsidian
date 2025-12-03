Any value when changed causes the UI to recomposed. Data that composable observe 

## `MutableState`
It is way to hold observable state
``` kotlin 
// creation
val counter = mutableStateOf(0)

// delegation 
var count by remember { mutableStateOf(0) } // Reading: count (reads value) // Writing: count = 1 (writes value)
```
## [[Remember]]
It is used to preserve state across recomposition 
## State Hoisting 
This make composable more reusable, testable and robust 
### Problem 
Storing mutable state directly in composable make it coupled to that specific component and it became harder to share. 
**Solution** - Move the state to a common parent or a `viewModel` 

## `rememberSaveable`
similar to [[Remember]] uses **Saved State Mechanism (`onSaveInstanceState`)** to persist state across process death 

## `derivedStateOf`
used when used state is derived from one or more other state variables . 
```kotlin 
val isEnabled by derivedStateOf { username.length > 5 && password.length > 8 }
```