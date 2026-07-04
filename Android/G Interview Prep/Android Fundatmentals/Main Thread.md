You can think of it as loop that continuously run which picks task and execute them one by one. 
## Why Single Thread 
- Guarantee UI consistency 
	- Multiple threads modifying UI will result in race condition 
	- Rendering become non-deterministic 
	- *Single Thread - predictable UI State*
- Avoid Locking Overhead 
	- You will need to lock everywhere 
- Event Driven Architecture 
	- Events (click, touch, lifecycle) they are process sequentially.
## Flow 
1. App Start -  Main thread is created
2. Looper is attached  - Looper run an infinite loop
	1. Takes message from message Queue (click, lifecycle events, runnable via handler ).  
	   *If queue is empty the thread blocks (waits) avoiding CPU waste. When arrives, it wakes up, process it and continues.*
	2. Executes it 
	3. Move to next 
## Why Android use Choreographer
Because rendering must be synchronized with display refresh rate, not executed as queue task. 
Message queue - generic task queue 
Rendering - time sensitive, frame aligned work 