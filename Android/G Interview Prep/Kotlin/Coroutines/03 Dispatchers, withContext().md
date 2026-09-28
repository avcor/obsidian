## Dispatchers 
It is a pool of thread on which coroutine will work on 
- **`Dispatchers.Main`** → UI thread (Android main thread)
- **`Dispatchers.IO`** → Thread pool for I/O operations (network, DB)
- **`Dispatchers.Default`** → For CPU-heavy tasks like sorting, parsing json, off main thread.
## withContext()
It is used to switch thread inside a coroutine
- blocking in nature i.e.  suspend the parent coroutine until withContext execution does not complete

> `Dispatchers.Default` is optimized for CPU-bound work and limits parallelism roughly around the number of available CPU cores. `Dispatchers.IO` is designed for potentially blocking operations and allows substantially higher concurrency because those operations may spend significant time waiting. The important distinction is not simply CPU versus network; it's whether the workload consumes CPU or blocks threads while waiting. Modern Kotlin coroutines use a shared scheduler underneath, but Default and IO apply different scheduling and parallelism policies.