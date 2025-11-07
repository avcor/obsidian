## Backpressure 
When producer emits faster than the consumer can consume. 
### Operator to handle 

#### 1.`buffer()` 
If buffer becomes full then producer is suspended until space is created in buffer.
Parameters 
1. `capacity` (default 0)
2. `onBufferOverflow` (default `BufferOverflow.SUSPEND`) 
	   - `SUSPEND`
	   - `DROP_OLDEST`
	   - `DROP_LATEST` 

```kotlin
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*
import kotlin.time.Duration.Companion.milliseconds

fun main() = runBlocking {
    println("--- Buffer Example Start ---")

    flow {
        // 🚀 Fast Producer: Emits a value every 10ms
        for (i in 1..5) {
            delay(10.milliseconds) 
            emit(i)
            println("Emitter: Emitted $i")
        }
    }
    .buffer(capacity = 2) // <-- Buffer size of 2
    .collect { value ->
        // 🐌 Slow Consumer: Takes 100ms to process a value
        println("Collector: Collecting $value")
        delay(100.milliseconds) 
        println("Collector: Processed $value")
    }

    println("--- Buffer Example End ---")
}
/*
### Expected Behavior
1. Emitter emits **1** (Buffer: [1]).
2. Emitter emits **2** (Buffer: [1, 2]).
3. Collector starts processing **1**.
4. Emitter emits **3**. Since the buffer is full, the producer coroutine is **suspended** at this point until space is made.
5. Collector finishes **1**, takes **2** (Buffer: [2] -> [2]).
6. Emitter resumes, emits **3** (Buffer: [2, 3]).
7. Collector finishes **2**, takes **3** (Buffer: [3] -> [3]).
8. Emitter emits **4** (Buffer: [3, 4]).
9. Emitter emits **5** (Buffer: [3, 4, 5]). **Wait!** With `capacity=2`, the emitter for **5** would be suspended again until the collector processes **3**.
*/
```
#### `conflate()`
drops intermediate emissions
#### `collectLatest()`
cancels previous collector when new item arrives 