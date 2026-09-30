- If one child fails then whole scope is cancelled, and it child also get stopped 
- `cancel()`  methods throw `CancellationException`, which cancels the child job if any other exception is thrown then whole parent job is cancelled.
- unhandled exception will eventually propagates to top hierarchy and it is delivered to thread which it started (usually main thread). This invokes JVM default unhandled exception mechanism which will terminate the application. 

## `launch`
 - propagates up in hierarchy 
 
```kotlin
GlobalScope.launch() { 
    val j1 = launch { 
        try { 
            Log.d(TAG, "onCreate: j1") 
        } catch (e: CancellationException) { 
            Log.d(TAG, "onCreate: caught") 
        } 
    } 

    Log.d(TAG, "can") 
    j1.cancel(); 
    // this will catch the exception 
}
```

```kotlin

val handler = CoroutineExceptionHandler { coroutineContext, throwable -> 
    Log.d(TAG, "onCreate: Handler") 
} 
val job = GlobalScope.launch(handler + Dispatchers.IO) { 
    val j1 = launch { 
        throw Exception("lol") 
        Log.d(TAG, "onCreate: j1") 
    } 
    Log.d(TAG, "can") 
    j1.cancel(); 
} 
// this will handle all the exception 
```

## `asynch`
- stored in deferred & re thrown at on await 
- 
```kotlin
val deferred = async { 
    throw IOException("Data not available") // Exception is held here
}
try {
    deferred.await() // Exception is re-thrown and caught here
} catch (e: IOException) {
    println("Handled deferred failure.")
}
//handler might not work as expected in async
```

## `SupervisorJob or supervisorScope { }` 
- Let child fail without cancelling 
- Exception is traveled up in hierarchy, it will be consider uncaught 
- Thus to prevent thread or app crash this must include [[#`CoroutineExceptionHandler`]] to gracefully handle or log that exception
  If it is missing then exception will be thrown when child coroutines finishes

## `CoroutineExceptionHandler`
- Job is to handle uncaught exception so that it wont crash the thread 
- It will not catch the exception which are thrown by [[#`asynch`]] as it will caught will try catch block. 

```kotlin
val handler = CoroutineExceptionHandler { context, exception ->
    println("Caught exception in ${context[CoroutineName]}: $exception")
    // Here you would usually log the error to a service like Firebase Crashlytics
}

val scope = CoroutineScope(Dispatchers.Default + handler)

scope.launch {
    // This exception will be passed to the 'handler' and logged.
    throw IllegalStateException("Background task failed.")
}
```