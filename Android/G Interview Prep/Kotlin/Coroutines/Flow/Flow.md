It is a reactive stream, 
- cold
	every collector triggers new execution of the flow's producer 
- asynchronous 
	asynchronously produces and consume without blocking the main thread
- sequential 
	- operation on flow are sequential and run in same coroutines where collection happens 
	- ==You can make it parallel using `flatMerge`==
``` kotlin
fun sequentialExample() = runBlocking {
    (1..3).asFlow()
        .onEach { print("Emitted $it, ") } // Operator 1
        .map { it * 2 }                  // Operator 2
        .collect { println("Collected $it") } // Terminal operator
}
/* Output:
Emitted 1, Collected 2
Emitted 2, Collected 4
Emitted 3, Collected 6
*/
```
- cancellable
	if collecting coroutines is cancelled, then the producer stop its work.

## Operators 
- `map`, `filter`, `take`, `reduce`, `flatMapConcat`, `flatMapMerge`, etc.
- `flowOn` changes dispatcher for upstream emissions.
### `flatMapConcat`
Flattening operator used to transform a flow of values into a single flow.
It Maps each value from outer flow into a new inner flow
```kotlin
fun postsFlow(userId: Int): Flow<String> = flow {
    println("  -> Start fetching posts for User $userId")
    delay(100) // Simulating a slow network/DB call
    emit("Post A by $userId")
    emit("Post B by $userId")
    println("  <- Finished fetching posts for User $userId")
}

fun main() = runBlocking {
    val userIds = flowOf(1, 2, 3) // The outer flow

    userIds.flatMapConcat { userId -> 
        postsFlow(userId) // Returns the inner flow
    }.collect { post ->
        println("Collected: $post")
    }
}

/*
 -> Start fetching posts for User 1
Collected: Post A by 1
Collected: Post B by 1
  <- Finished fetching posts for User 1
  -> Start fetching posts for User 2  <-- Only starts after User 1 finishes
Collected: Post A by 2
Collected: Post B by 2
  <- Finished fetching posts for User 2
  -> Start fetching posts for User 3
Collected: Post A by 3
Collected: Post B by 3
  <- Finished fetching posts for User 3
*/
```

### `flatMapMerge`

```kotlin
fun fetchProfile(userId: Int): Flow<String> = flow {
    val delayMs = (4 - userId) * 100L // User 3 is fastest (100ms), User 1 is slowest (300ms)
    println("  [START] Fetching profile for User $userId (will take ${delayMs}ms)")
    
    // Simulates the concurrent, suspending work
    delay(delayMs) 
    
    emit("✅ Profile for User $userId received")
    println("  [END] Finished User $userId")
}

fun main() = runBlocking {
    val userIds = flowOf(1, 2, 3) // Outer flow

    println("--- Starting concurrent fetching ---")
    
    userIds
        .flatMapMerge { userId -> 
            fetchProfile(userId) // Starts collecting this inner flow concurrently
        }
        .collect { result ->
            // Results are collected as soon as they arrive
            println("Collected Result: $result")
        }
    
    println("--- All profiles collected ---")
}

/*
--- Starting concurrent fetching ---
  [START] Fetching profile for User 1 (will take 300ms)
  [START] Fetching profile for User 2 (will take 200ms)
  [START] Fetching profile for User 3 (will take 100ms)
  [END] Finished User 3
Collected Result: ✅ Profile for User 3 received
  [END] Finished User 2
Collected Result: ✅ Profile for User 2 received
  [END] Finished User 1
Collected Result: ✅ Profile for User 1 received
--- All profiles collected ---
*/
```