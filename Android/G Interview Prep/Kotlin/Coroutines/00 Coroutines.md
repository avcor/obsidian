
## 1.Program
- Set of instruction 
## 2.Process 
- Instance of program running in memory 
- Process Id 
- State - New, Run, Ready, Pause, Terminate
- Runs in memory with help of thread
## 3.Thread
- Smallest unit of execution within a process 
- These are heavy has its own stack of memory ~2MB or 1MB
- There are finite number of thread that we can make depending on system.
## 4.Coroutines
- These are programming block that allows to write asynchronous, non blocking code sequentially.
- These are lightweight threads but not exactly threads 
- It can pause execution (suspend) without blocking thread and resume later, allowing efficient use of limited thread. 
- *Dispatchers.Default uses multiple thread.* This could provide parallelism 
	Look at [[Concurrency & Parallelism]]
- Why over RxJava 
	Easier concurrency, cancellation plus better integration  with kotlin's language suspend system 
## [[02 Suspend|5.suspend]]

## 6.Job
- Unit of work, every coroutine is associated with it. 
- **Custom job** act as a parent job for coroutine scope 
- **By default it works on Dispatcher.Default, when no dispatcher is specified**

What problems it solves
1. Cancellation support 
2. Making them cheap 
3. Thread problems 
4. Context Switching not possible in thread, you can do it withContext(Dispatchers.Main) or child jobs 
