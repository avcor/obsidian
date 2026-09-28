It is synchronisation mechanism that make sure that only one thread can enter a section of time. 
It is coroutine friendly. 
It solves the same problem as [[Synchronization]]

```kotlin 
val mutex = Mutex()
var counter = 0

suspend fun increment() {
    mutex.withLock {
        counter++
    }
}
```

## Why it used 
In synchronised block - the monitor blocks the thread but in mutex suspend, it allows underlying thread to do other work. 
This becomes helpful when dealing with android's limited thread pool and coroutines. 