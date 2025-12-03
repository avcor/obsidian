- It is used to manually trigger an coroutine in response to UI event (like button click) 
- These UI events are outside of composable's lifecycle management. 

- It returns a `CorutineScope` that is bound to composition
- When composable leaves the composition, the returned scope is cancelled

## Use 
- It can be used to launch coroutines where from non composable lambda function. 
- E.g. launching a coroutine to scroll to position in lazy column from a lambda of a button click 

```kotlin 

@Composable
fun ScrollButton() {
	val scrollState = rememberScrollState()
	
    val coroutineScope = rememberCoroutineScope()
    Button(onClick = {
        coroutineScope.launch {
            scrollState.animateScrollToItem(index = 0)
        }
    }) {
        Text("Scroll to Top")
    }
    
    Coloumn(modifier = Modifier.verticalScroll(scrollState)) {
	    // display item
    }
}
```

## Why [[launchedEffect]] can not be used in onClick() 
LaunchedEffect is a composable function and composable function can only be called from another composable function. But  `onClick` is not a composable function 