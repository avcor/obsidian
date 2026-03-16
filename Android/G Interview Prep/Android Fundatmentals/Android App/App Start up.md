Types [[#Cold Start]], [[#Warm start]], [[#Hot start]] 
Metric which decide app startup are 
### Time to Initial Display (TTID) 
- Time to take display first frame - loading 
- From process fork -> First frame drawn 
### Time to Fully Drawn (TTFD)
- Time to take fully interactive - actually usable 
- First frame -> To fully interactive 
- Tools to measure `Perfetto`
## Cold Start
- It refers to app launching from scratch (app launching for first time and earlier system killed it)
- Sequence
	- [[Android App#How application is loaded#Process before app loaded|Process before app loading]]
	- [[Android App#How application is loaded#During app load|App Load]]
- When app process completes the first draw, the system process swaps out [[#Starting-loading window]] background window with main activity

## Warm start 
- It is a subset of operations that take place during cold star.
- When system evicts some memory but core parts of the process can be reused.
- System task has memory of what app was doing.
Why after process death involves creating a new process, it is still warm that cold 
1. It receives `bundle` with UI state. This allow app to skip intro screens and jump back to where user was 
2. System keeps the app in recent screen. It does not have to look for Launcher activity. It already knows which screen was at the top and tries to recreate that specific directly. 
3. System knows it is restoring a session it can use cached information about app's component that would not be true cold start. 
## Hot start 
- System brings your activity from background to foreground
- App process and your activity both are still alive in background, activity skips `oncreate()` and just triggers `onRestart() -> other callbacks`
- If some memory is purged in response to memory trimming then objects (lets say bitmap or list of items) then objects needs to be recreated. You will see app UI immediately but it might blank inside e.g. white spaces where images should be until logic fetches those again.

## Cold start feel slow 
### If activity code is fast 
Because app is launched from scratch as described in [[#Cold Start]]
### If activity is not fast
- Too much initialization on Application `onCreate()` 
	- DB init on main thread 
	- Network call on startup 
	- Disk I/O on Main thread
	- Reading `sharedPrefrences`
## Interview Question 
How to answer
- First determine the problem is app-caused or system-caused
- Say what will you optimize first 

