>Dispatcher will work only in async calls. 

- OkHttp does not create unlimited threads. 
- It has a Dispatcher that manages asynchronous request and the threads that is used to execute them. 

It manages things like 
- Currently running asynchronous requests
- Queued request
- Concurrent requests
- Thread usage

> The dispatcher is responsible for managing async execution and its thread pool. But sync calls are executed on caller's thread even though it also track sync calls for bookkeeping and cancellation/shutdown related management. 
