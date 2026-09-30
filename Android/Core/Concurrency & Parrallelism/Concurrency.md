Requisites 
- [[00 Coroutines#2.Process |Process]] 
- [[00 Coroutines#3.Thread|Thread]]
## Context Switching 
Condition - 1 CPU core has 3 threads 
- CPU cannot execute all three instruction simultaneously
- OS scheduler gives each thread some time on CPU 
- When CPU switches b/w thread, this is called context switching. 
Problem 
- CPU has to preserve state for thread A so that it can be resumed later. 
- Then it loads B's state then switch again 
- It has overhead
*More threads does not mean better performance*

## Race Condition 
- [[Synchronization]]
- [[Atomic Variables]]
- [[Mutex]]
