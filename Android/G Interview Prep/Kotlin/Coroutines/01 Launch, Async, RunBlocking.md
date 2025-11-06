These builder create and start coroutines

## launch
- Fire and forget, 
- Returns job 
- ***join() or joinAll()*** works  job Object for suspending the current coroutine until child coroutine completes the job.

``` kotlin
runBlocking {
    val jobs = listOf(
        launch { doWork(4000) }, // Job A (4 seconds)
        launch { doWork(1000) }, // Job B (1 second)
        launch { doWork(2500) }  // Job C (2.5 seconds)
    )
    // The current coroutine suspends until ALL jobs in the list complete.
    jobs.joinAll() 
    println("All concurrent tasks are finished.") 
    // Total Time taken: MAX(4s, 1s, 2.5s) = 4 seconds
}
```

## async 
- [[Concurrency & Parallelism|Concurrent]] execution that returns `Deferred<T>` future value. Expect result from coroutine
  In real world scenario if it is doing heavy work or holding some resources and fails to call await then it can lead to resource leak if parent job completes without waiting for or cancelling the child async job. 
  The parent scope finishes _so quickly_ that the child task hasn't had time to even register the cancellation and release the resource.
  [[02 Suspend#Work leak| work leaks]]
- If await is **not called** coroutines still runs but the exceptions inside it are lost unless awaited 

```kotlin
runBlocking {
    val job = launch {println("Task A")}
    val deferred = async {"Task B result"}
    job.join()
    //println(deferred.await())
}
```

```kotlin
suspend fun fetchUserData(): String { /* ... takes 4000ms ... */ return "User Data" }
suspend fun fetchPaymentHistory(): String { /* ... takes 1000ms ... */ return "History" }

runBlocking {
    // 1. Launch all tasks concurrently
    val deferredResults = listOf(
        async { fetchUserData() },       // Starts running (4s)
        async { fetchPaymentHistory() },  // Starts running (1s)
        async { "Static Result" }
    )
    // 2. Await all results simultaneously
	// Return type for all are string if this is not the case then await on individually 
    val results: List<String> = deferredResults.awaitAll()
    // Total time taken: MAX(4s, 1s, 0s) = 4 seconds
    println("Total results: $results")
    // Output order is preserved: [User Data, History, Static Result]
}
```
## runBlocking 
- Blocks the current thread until all its coroutines complete.
- Usually in Test and Main function 

