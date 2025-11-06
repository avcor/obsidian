
- It is function which paused and resumed later. It is called from another suspend function or coroutines. 
- When suspend hits `delay` it does not block the thread it stores the current continuation and frees up current thread. 
- kt keep track of function running and its variable, in a stack. when resumed it copies from stack and start running again.
- [[#yield()]]
## yield()
It tells the dispatcher that it is okay to pause here, let other run before I continue. The long running coroutine can block other from running on same dispatcher thread. 
`Dispatcher.Default` has limited number of thread, usually = CPU cores 

- Checks for cancellation 
  If cancelled - throw `CancellationException`
  If active suspend temporarily and re-schedule continuation on same dispatcher
- Gives up the thread to let other coroutines run first
- Resume back when the dispatcher thread become free 

*yields() more often, can slightly reduce raw throughput.*

```kotlin
launch(Dispatchers.Default) {
    for (i in 1..1_000_000) {
        if (i % 1000 == 0) yield() // give CPU time to others
        heavyComputation(i)
    }
}
```

## isActive 
- A boolean which tells if coroutine is running or not
## ensureActive()
- A function that checks if the coroutines is active if not then throw `CancellationException`
- It is the right way to stop it
- Automatically cleans the coroutine chain
- Triggers parent job cancellation and cleanup

```kotlin 
val job = launch {
    try {
        heavyComputation()
    } finally {
        println("Cleaning up resources")
    }
}
delay(100)
job.cancelAndJoin()

suspend fun heavyComputation() {
    for (i in 1..1000) {
        ensureActive() // throws CancellationException
        doWork(i)
    }
}
```
`CancellationException` propagates up and parent job knows it was cancelled 

## Work leak 
==Why does loop does not stop when coroutine is cancelled==
- ==It will only stop at next suspension point i.e (delay(), await() ,yield())==
- ==If loop never suspends then it never notice it was cancelled== 

==**Work leak** : coroutines that has been lost, it can resume itself to use. waste cpu, launch network request==
