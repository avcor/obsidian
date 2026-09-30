Android kills the app process to reclaim memory. It is an OS level kill so no [[Activity Lifecycle|lifecycle]] callbacks are called. **OS-level memory reclamation decision**, not an app lifecycle event.
When process death happens entire heap is wiped
## Triggers 
> Android ranks processes using **importance levels** (foreground, visible, service, background, cached). The system kills the **least important processes first**, usually cached or long-backgrounded apps. OEMs may apply more aggressive policies, but the base decision is driven by process importance and resource pressure.

- App in background, & low memory
- User has not used app recently 
- OEM aggressive killing 
- Thermal pressure 
``` sequence
App goes to background - Process Killed (Memory wiped)
User returns to app 
New process start - New Application - New Activity  
```
[[ViewModel#Cases#Process death]]
>UI state must be restorable. Business state must be recoverable.
## Why process kill without [[Activity Lifecycle#onDestory()|onDestroy()]]
This is intentional design , not laziness 
Why not just call 
- It will require 
	- Switching threads 
	- Running user code 
	- Risking ANRs 
	- Delaying memory claims 
- OS priority > app lifecycle. System cannot be polite to the app
### Questions 
Q Why not keep `ViewModel` across process death ?
- It is a memory construct, process - bound, lifecycle aware, UI state holder. 
- It's responsibility is to survive configuration changes, not process death. 
- When process death happens entire heap is wiped out, objects are gone, no lifecycle callback called.
	- Keep it would require entire object, restoring later. This is not view model is meant for. 
- Android must remain free to kill process instantly, reclaim memory aggressively, prioritize system responsiveness. If this would be requirement then android need to coordinate with app before killing them, which will make the process slow, because serializing comes at the cost which can cause the UI freezes or ANR. If you want to store small UI states then [[ViewModel#Cases#Process death]] it is a better choice.
	- View models often hold non-serializable resources (Flow or coroutines), serializing them will hamper performance
	- Keeping view model will risk stale state or corrupted state. Explicit restoration is better  