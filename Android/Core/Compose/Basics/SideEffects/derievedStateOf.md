It decides the state on the basis of one or more states and only triggering recomposition if result is changed. 
## Key characteristics 
- State Calculation - result depends on one or more state  
- Optimization -  recomposition only happens when the result is changed 
- Lazy Evaluation - calculation block runs when read first time or one of the source state is changed 
## When Does not help
- Computation is cheap 
- Input changes rarely 
- Value not used in UI (no recomposition benefits)
> It is not useful when recomposition frequency is low or computation is cheap, because the overhead of state tracking outweighs its benefits. 
## Scope 
The calculation in inside `derievedStateOf` is run within the same snapshot system as recomposition, ensuring thread safety and tracking of state reads 

``` kotlin 
@Composable
fun ScrollToTopButton() {
	val listState = rememberLazyListState()
	val scope = rememberCoroutineScope()
	
    val isButtonVisible by remember {
        derivedStateOf {
            listState.firstVisibleItemIndex > 10
        }
    }

    AnimatedVisibility(visible = isButtonVisible) {
        Button(onClick = { 
			scope.lanuch {
				scrollState.animateScrollToItem(0) 
			}        
        }) {
            Text("Scroll Up")
        }
    }
}
```