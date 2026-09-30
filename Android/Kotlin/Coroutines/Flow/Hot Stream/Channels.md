- Channels are hot, concurrent pipelines for sending and receiving data between coroutines. 
- It is like a queue 
- **When you send to closed channel it throws `ClosedSendChannelException`**

**How it concurrent ?**
It achieves  by providing suspending, thread-safe mechanism for communication between coroutines 

`send()` & `receive()`

- **Rendezvous (default)** — No buffer; sender suspends until receiver ready.
- **Buffered** — Allows limited buffering.
- **Conflated** — Keeps only the latest value.
- **Unlimited** — Never suspends (dangerous).

```kotlin
val channel = Channel<Int>()

launch {
    for (x in 1..5) {
        channel.send(x)
        println("Sent $x")
    }
    channel.close()
}

launch {
    for (y in channel) {
        println("Received $y")
    }
}
```

## Where it is used 
It ensure that message is gone once and receiver takes it. It is good showing toast, or snackBar messages. When we use StateFlow it will show the message when screen orientation changes as it store the last update, hence after the re-layout toast might be displayed again. 

## Select Expression 
It allows to wait for winner completion of suspend function complete first
```Kotlin
import kotlinx.coroutines.*
import kotlinx.coroutines.selects.* 

fun CoroutineScope.data1(): Deferred<String> = async {
    delay(1000L) // 1 second delay
    "Data 1 (The Winner)"
}

fun CoroutineScope.data2(): Deferred<String> = async {
    delay(2000L) // 2 second delay
    "Data 2 (The Loser)"
}

fun main() = runBlocking {
    println("Starting race between two data sources...")
    val winner: String = select {
        data1().onAwait { result ->"Result: $result"}
        data2().onAwait { result ->"Result: $result"}
    }
    println("Race finished. The selected result is: $winner")

    // IMPORTANT: Since select only waits for the winner, the other coroutine (data2)
    // is still running unless you explicitly cancel its children.
    coroutineContext.cancelChildren()
}
/*
Starting race between two data sources... Race finished. The selected result is: Result: Data 1 (The Winner)
*/
```

