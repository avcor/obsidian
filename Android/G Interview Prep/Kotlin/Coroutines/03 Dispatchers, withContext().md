
## Dispatchers 
It is a pool of thread on which coroutine will work on 
- **`Dispatchers.Main`** → UI thread (Android main thread)
- **`Dispatchers.IO`** → Thread pool for I/O operations (network, DB)
- **`Dispatchers.Default`** → For CPU-heavy tasks like sorting, parsing json, off main thread.


## withContext()
It is used to switch thread inside a coroutine
- blocking in nature i.e.  suspend the parent coroutine until withContext execution does not complete
