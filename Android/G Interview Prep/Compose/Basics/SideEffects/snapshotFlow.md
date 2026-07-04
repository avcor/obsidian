- It is a reverse of [[produceState]] 
- It converts the composable state into kotlin flow 

## characteristics 
- It launches a block that runs whenever the read compose state changes 
- The block runs inside the compose [[SnapShot#Snapshot System|snapshot system]] ensuring that any read state is observed

```kotlin 
@Composable 
fun SearchComponent() {
	var text by rememberSaveable { mutableStateOf("") }
	
	TextField(
		value = text,
		onchange = {text = it }
	)
	
	val qFlow = snapshotFlow { text }
	
	LaunchedEffect(Unit) {
		qFlow.filter(it>5).collect {print("$it")}
	}
}
```