A coroutine runs within the context, which is key-value map pair that hold everything about that coroutine.
- [[00 Coroutines#6.Job|Job]]
- [[03 Dispatchers, withContext()#Dispatchers|Dispatchers]]
- Name 
- Any custom context elements 

*coroutines inherit context from its parent, except for elements you override *

``` kotlin
data class RequestId(val id: String) : CoroutineContext.Element {
    companion object Key : CoroutineContext.Key<RequestId>
    override val key: CoroutineContext.Key<*> get() = Key
}

val ctx = Dispatchers.IO + RequestId("REQ-2025-101") + CoroutineName("Downloader")

launch(ctx) {
    println("${coroutineContext[RequestId]?.id}")
    println("Running in ${coroutineContext[CoroutineName]?.name}")
}
```

