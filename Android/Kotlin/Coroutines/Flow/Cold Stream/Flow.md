It is a reactive stream, 
- cold
	every collector triggers new execution of the flow's producer 
- asynchronous 
	asynchronously produces and consume without blocking the main thread
- sequential 
	- operation on flow are sequential and run in same coroutines where collection happens 
	- ==You can make it parallel using [[Flow Operator#`flatMapMerge`|flatMapMerge]]==
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
- `map`, `filter`, `take`, `reduce`, [[Flow Operator#`flatMapConcat`|flatMapConcat]], [[Flow Operator#`flatMapMerge`|flatMapMerge]] etc.
- `flowOn` changes dispatcher for upstream emissions.
-  For other visit [[Flow Backpressure]]
