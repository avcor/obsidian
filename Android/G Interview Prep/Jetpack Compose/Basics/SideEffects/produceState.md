It is a function that is used to convert non - composable state (flow, live data stream ) into composable state object 

 ***Note - You can use `collectAsState` instead of this***
*A produce state is just composable with [[remember]] and [[launchedEffect]]* 
## Characteristics 
- State production - It launches a coroutines  in which you can call a suspend function and emit multiple values. **Coroutines is similar to [[launchedEffect]]  coroutine scope** 
- Return Type - It return `State<T>` object. Reading it trigger recomposition 
- Key - It triggers when Key is started 

## Example with `produceState`
``` kotlin 
@Composable
fun postCard(id: String) {
	val post by produceState<Result<Post>?>(initialValue = null, key = id) {
		value = getPostInfo(id)
	}
	
	if(post == null) {
		// loading
	} else {
		post?.success {
			
		}?.failure {
			
		}
	}
	
}

fun getPostInfo(id: String): Result<Post> {
	return withContext(Dispatchers.IO) {
		delay(3.seconds)
		Result.success(
			Post(id="id1", name="hello")
		)
	}
}
```

## Example without `produceState`
```kotlin
@Composable
fun postCard(id: String) {
	var post by remember { mutableStateOf<Result<Post>?>(null) }
	
	LaunchedEffect(key = id) {
		post = getPostInfo(id)
	}
}

fun getPostInfo(id: String): Result<Post> {
	return withContext(Dispatchers.IO) {
		delay(3.seconds)
		Result.success(
			Post(id="id1", name="hello")
		)
	}
}
```