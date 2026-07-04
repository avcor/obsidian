## Fast and idempotent 
1. They should not do complex work like network calls 
2.  Calling function with same argument must produce the same result. They must not rely on state that is managed by compose 
``` kotlin
val globalCounterFlow = MutableStateFlow(0) 
@Composable
fun FlowCounter() {
    Column() {
// right way 
// val counter by globalCounterFlow.collectAsState()
        Text(text = "Count: ${globalCounterFlow.value}") 
        Button(onClick = {
            globalCounterFlow.value++ 
        }) {
            Text("Increment (Still Doesn't Work)")
        }
    }
}
```

## Side-effect free 
They should not do any task such as write to db or update in `viewModel` directly inside the body. All the side effects should be in function like `LaunchedEffects` or `rememberCoroutineScope`

Do not put any expensive operation in composable.
## Composable run in any order 
There is no guarantee in the order of execution. 

## Composable skip 
Do not rely on composable that it will run your task every time 

## Call 
Composable can be called from another composable function or `CompositionLocalScope`
